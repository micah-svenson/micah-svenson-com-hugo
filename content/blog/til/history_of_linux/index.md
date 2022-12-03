---
title: "What's a Fork Bomb?"
date: 2022-11-20T00:00:00-00:06
draft: true
tags: TIL
---

I was scrolling the depths of r/programminghumor when I came across a strange and quite incomprehensible line of code

```
:(){ :|:& };:
```

After whipping out google, it turns out this is known as a fork bomb. 

The specific line of code is not the original formulation of the fork bomb, but is a popularized version written by Jaromil. Interestingly, his goal was to encode this virus as "work of art"


A fork bomb makes use of bash and process forking to overwhelm a systems cpu resources (among other things), effectively creating denial of service.

The fork bomb is more clearly understood like this

```
fork_bomb(){
    fork_bomb | fork_bomb&
};
fork_bomb
```

First, a bash function is defined ( `fork_bomb(){};` ) with no input arguments and then immediately called afterwards ( `fork_bomb` ). The function recursively calls itself and pipes the result to another recursive call that is then sent to the background as a daemon process ( `fork_bomb | fork_bomb&` ). 

Lets step through how these lines of code lead to a denial of service attack. Although the premise of the attack is generally intuitive, it took a minute for me to fully understand all of the mechanisms.

Initially my main questions were:
1. Why use a pipe when the function has no output?
2. Why is it necessary to send the processes to the background?
3. Why not add more calls using &&? i.e. `fork_bomb && fork_bomb ...`

### The Pipe




## Are forkbombs an actual threat in modern times?


