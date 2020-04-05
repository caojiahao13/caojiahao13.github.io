---
layout: default
title: "Jiahao Cao's homepage"
description: An unknow random process
theme: jekyll-theme-cayman
---

I was trying to simulate a Markov chain with transition matrix：

$$\begin{aligned}
&\begin{array}{ccccc}
& 1 & 2 & 3 & 4 \\
1 & 0.2 & 0.7 & 0.1 & 0 \\
2 & 0.05 & 0.1 & 0.05 & 0.8\\
3 & 0 & 0 &1 &0 \\
4 & 0 & 0 &0 &1
\end{array}
\end{aligned}$$

Theoretically, we know state 1 eventually be absorbed by state 3 with probability $\frac{25}{137} $。Here is my simulation:

```
M = 10000
np.random.seed(1234)
final_state = np.zeros(M)
for i in range(M):
    x = 1 # start from 1
    while(True):
        r =st.uniform.rvs()
        if(x==1):
            if(r<0.2):
                x = 1
            elif(r<0.9):
                x = 2
            else:
                x = 3
                break
        if(x==2):
            if(r<0.05):
                x = 1
            elif(r<0.15):
                x = 2
            elif(r<0.2):
                x = 3
                break
            else:
                x = 4
                break
    final_state[i] = x
p1 = np.sum(final_state==3)/M
print(p1)
```
While the result did not agree with what I expected. So I checked my code and find I used a single random number to determine how to change to next step given different start state. This could be the problem so I changed it :
```
M = 10000
np.random.seed(1234)
final_state = np.zeros(M)
for i in range(M):
    x = 2# start from 1
    while(True):
        if(x==1):
            r =st.uniform.rvs()
            if(r<0.2):
                x = 1
            elif(r<0.9):
                x = 2
            else:
                x = 3
                break
        if(x==2):
            r =st.uniform.rvs()
            if(r<0.05):
                x = 1
            elif(r<0.15):
                x = 2
            elif(r<0.2):
                x = 3
                break
            else:
                x = 4
                break
    final_state[i] = x
p1 = np.sum(final_state==3)/M
print(p1)
```
Then I got the right answer.  Here my problem is , what kind of process does the first version code determine? Is there any examples of this process in real life?
