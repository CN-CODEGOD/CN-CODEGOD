# BFS(breath deep search)


BFS is a deep search method that recall all the path from graph

we have a new graph has different node ,
and we have a start node 0, we first search node 0's neighbor and we deque the visted node and keep go on untill all node was visted
![image](https://github.com/CN-CODEGOD/CN-CODEGOD/assets/166476136/cb7111cc-c6fc-43fa-8a9c-8af2d7cba0aa)

we want to explore all the unvisted neighbor of 0 and add them to the Q which is 9 11 7

![image](https://github.com/CN-CODEGOD/CN-CODEGOD/assets/166476136/ef65ca1e-6e34-4401-bbea-d9e5bfedfaf1)

so 0 have no more unvisted neighbor

and we move on ,9 is next up to the Q ,so we add all 9's unvisted neighbor to the Q
SO that is 10 and 8
![image](https://github.com/CN-CODEGOD/CN-CODEGOD/assets/166476136/770098f0-1e3b-4486-9c14-c15187489b6e)

and we move on to the next node in our  Q which is 7 ,SO we add all 7 unvisted neighbor to the Q, SO we try to vist node 11 but node 11 is already in the Q ,SO we skip it, we add 6 in the Q  and 3 to the Q ,this process goes on and on untill we run out of Q

## ALL posible BFS

in above case , the BFS isn't recall all posible path 

e.
7
