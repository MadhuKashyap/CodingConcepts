#### This method is used to detect cycle in undirected graph

1. Initially create subsets containing only a single node which are the parent of itself.
2. while traversing through the edges, if the two end nodes of the edge belongs to the same set then they form a cycle.
3. Otherwise, perform union to merge the subsets together. (make parent of 1 subset the parent of another subset)

![image](https://github.com/user-attachments/assets/f04d0e2e-8f6d-4da0-a75c-d6a5a4d668e1)

 
