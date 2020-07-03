---
title: "Binary Tree"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
# Implement a binary tree data structure


```python
class Node:
    
    def __init__(self, content=10):
        self.content = content
        self.right = None
        self.left = None 
        
    def sum_nodes(self):
        """ Return the sum of contents in all nodes"""
        sum = self.content
        if self.right != None or self.left != None:
            #do something
            sum += self.right.sum_nodes() + self.left.sum_nodes()
        #else:
            #do something
        return sum
        
    
node = Node(10) 
print(node.content)

node_right = Node(11)
node_left = Node(12)

node.right = node_right
node.left = node_left 

print(node.sum_nodes())

```

    10
    33

