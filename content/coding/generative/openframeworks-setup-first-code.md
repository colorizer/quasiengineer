---
title: "OpenFrameworks Setup & First Code"
date: 2023-03-01T09:08:45+05:30
draft: false
katex: true
tags: ["Coding", "Art"]
categories: ["⌨️ Coding", "🎨 Generative"]
summary: ""
typora-root-url: ../../../static
---

I've been interesting in generative coding or creative coding for a long time spending my time in the different alleys of subreddits. So, I finally decided to venture into this using the opensource C++ toolkit called [OpenFrameworks](https://openframeworks.cc/). This post will have a short guide on installing the toolkit and my first code written using it.

## Installation

This won't be a comprehensive guide but rather points to stuff that needs to be done to get it running (as of today) on Linux.  

1. The OpenFrameworks community [recommends latest nightly over 0.11.2, the current stable version](https://forum.openframeworks.cc/t/note-nightly-builds-recommended-over-0-11-2/41220).  You can find nightly builds at the bottom of: [download | openFrameworks](https://openframeworks.cc/download/).
2. On the same download page, you can find the link for instructions to install ([Here's the link for Linux instructions](https://openframeworks.cc/download/)).
3. There's a high chance that you might face some issue related to `SNDFILE` while compiling using `compileOF.sh` file. The fix for the same can be found over at [this patch file](https://gist.github.com/kerrickstaley/7f8c65a27a1f4e79a942235b87c1f0c0) (I found the patch file through the comment section of the coresponding [AUR package](https://aur.archlinux.org/packages/openframeworks)). You can either apply the patch (I don't know, as of now) or apply it manually since its only 2 lines of code related to linking header files.
4. You should also setup the **Project Generator** and the **QT Creator** IDE.

Please note that the libraries in OpenFrameworks uses relative reference for files and folders with respect to the parent folder where the package is extracted and compiled. Hence, it is easier to compile the code if your project is present in the `OF/apps/myApps/` folder where `OF` is the extracted folder.

Also, I personally use VSCode and makefile for editing and running the code since qbs (QT Creator) was having multiple issues related to linkage of library. With these issues discussed, let's move on to my first code.

## First Code

### Concept

The idea is to generate a "*spiral of squares*" if that makes any sense. It was actually inspired by a similar hand-drawn art that I saw while scrolling through instagram (sorry, couldn't share source). What we are going to do is to create a simple trignometric math around the concept and then implement the same as part of the code. The idea is as follows:

![Square Spiral Idea](/images/2023/openframeworks-setup-first-code/square_spiral_idea.jpg "Black text corresponds to nodes and the blue text corresponds to dimensions")

Each of the distances in the above diagram can be derived based on three parameters - $w, h, \theta$.

- $p = w\tan\theta$.
- $q = h - p$
- $r = q\tan\theta$
- $s = w - r$
- $t = s\tan\theta$
- $u = h - t$
- $x = u\cos\theta\sin\theta$
- $y = u\sin^2\theta$

Then, the nodes can be represented as points in space with node "**a**" as origin.

- $a = (0,0)$
- $b = (w,0)$
- $c = (w,h)$
- $d = (0,h)$
- $e = (w,p)$
- $f = (s,h)$
- $g = (0,u)$
- $i = (x,y)$

The idea is to initially set the point **a** as origin and compute all the points relative to that. Then, after connecting all the points, we can set the point **i** as the next origin and change the orientation by **$\theta$**. Thus, the inner square/rectangle becomes the starting point for the next iteration.

### Implementation

For the implementation, there are three major code files in the project folder.

```tree
└── src
    ├── main.cpp
    ├── ofApp.cpp
    └── ofApp.h
```

The `main.cpp` file is the one which actually executes the program. The `ofApp.h` is a header file which is mainly used to declare the `ofApp` class and its corresponding functions. The actual definitions of these classes exist in the `ofApp.cpp` file. For example, `setup()` function is used to define static objects such as background and `keyPressed(key)` is used for events related to keypress.

```c++
void ofApp::setup(){
    ofSetWindowShape(920,1080);
    ofColor bg;
    bg.setHsb(200, 120, 80);
    ofSetBackgroundColor(bg);
    ofEnableAntiAliasing();
}
```

In order to take save the generated output as an image, we declare an `ofImage` object in the `ofApp.h` file as below.

```c++
class ofApp : public ofBaseApp{

	public:
		void setup();
		void update();
		void draw();
        ...
        ...
		ofImage img;

		
};
```

Then, we update the following function in `ofApp.cpp` as follows:

```c++
//--------------------------------------------------------------
void ofApp::keyPressed(int key){
    if(key == 'x'){
        img.grabScreen(0, 0, ofGetWidth(), ofGetHeight());
        img.save("screenshot.png");
    }
}
```

Now, for our drawing, we update the `draw()` function. This function is executed for every frame. Hence, though it is a static image, it will still be updated relative to the window size. I've put the code below and commented it to reflect my indent on doing so.

```c++
void ofApp::draw(){
    // Set the line properties.
    ofSetLineWidth(4);
    ofNoFill();
    ofColor linecolor;
    linecolor.setHsb(245, 40, 230);
    ofSetColor(linecolor);

    float w = ofGetWidth(), h=ofGetHeight();
    float theta = PI/75; // Set the angle in radian
    ofPoint a, b, c, d, e, f, g, i;
    float p, q, r, s, t, u, v, x;

    // Draw the initial rectangle and the rest of the inner spirals.
    ofDrawRectangle(0,0, w, h);
    for(int z=0; z<50; z++){
        a.set(0,0);
        b.set(w,0);
        c.set(w,h);
        d.set(0,h);
        p = w*tan(theta);
        e.set(w,p);
        q = h - p;
        r = q*tan(theta);
        s = w-r;
        f.set(s, h);
        t = s*tan(theta);
        u = h-t;
        g.set(0,u);
        v = u*cos(theta)*sin(theta);
        x = u*sin(theta)*sin(theta);
        i.set(v,x);
        ofDrawLine(a,e);
        ofDrawLine(e,f);
        ofDrawLine(f,g);
        ofDrawLine(g,i);
        // Update the width and height for the next iteration.
        w = i.distance(e); 
        h = e.distance(f);
        ofTranslate(i); // Translate to i relative to the current origin.
        ofRotateRad(theta); // Rotate the orientation of the co-ordinate system by theta.
    }
    
}
```

This code has resulted in the following spiral, my first ever creative generation!

![Spiral of squares](/images/2023/openframeworks-setup-first-code/openframeworks_spiral.png "Spiral of Squares")