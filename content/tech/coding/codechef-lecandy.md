---
title: "Codechef LECANDY"
date: 2021-08-24T12:33:45+05:30
draft: false
katex: false
tags: ["Coding",]
categories: ["🗃️ Tech", "⌨️ Coding"]
typora-root-url: ../../../static
---

**Problem Statement**: [Link](https://www.codechef.com/problems/LECANDY)

The following are my solutions to the problem statement.

##  C++

```c++
#include <iostream>
#include <vector>
#include <string>

using namespace std;

int main() {
    int T, N;
    unsigned long int C, C2, temp;
    cin >> T;
    vector<string> arr(T);

    for(int i=0; i < T; i++){
        cin >> N >> C;
        C2 = 0;
        for (int j=0; j < N; j++){
            cin >> temp;
            C2 += temp;
        }
        if (C2 > C)
            arr[i] = "No";
        else
            arr[i] = "Yes";
    }

    for(auto& i: arr)
        cout << i << endl;

    return 0;
}
```

## Python

```python
def possible(N,C):
    C_wish = sum(map(int, input().split()))
    if C_wish > C:
        return 'No'
    else:
        return 'Yes'
 

T = int(input())
ANS = []

for _ in range(T):
    N, C = map(int, input().split())
    ANS.append(possible(N,C))
    
for an in ANS:
    print(an)
```



