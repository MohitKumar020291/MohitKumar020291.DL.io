# Tensor Implementation from Scratch

## Introduction

This project aims to create tensors from scratch, with the backend written in C++ and the wrapper API in Python. We're exploring the use of YAML to invoke the backend using Python instead of pybind11.

## What are Tensors?

Tensors are multidimensional arrays or vectors with more than two axes. They are fundamental to many areas of mathematics, physics, and computer science, particularly in machine learning and data analysis.

## Basic Tree to Tensors Approach

We're using a tree-based approach to understand and implement tensors. Here's how it works:

1. We start with a general tree architecture using a normal list.
2. Each node in the tree represents a dimension or element of the tensor.
3. The structure of the tree corresponds to the shape of the tensor.

### Example: Single Child Tree Implementation

Here's a simple C++ implementation of a single-child tree:

```cpp
#include <iostream>
#include <vector>
#include <string>

class SingleChildTree{
    public:
        std::vector<char> Tree;
        int size;

        void createTree() {
            std::string tree;

            std::cout << "Enter nodes (single character sperated by a space): ";
            std::getline(std::cin, tree);

            for(char node : tree) {
                if (node != ' ') {
                    Tree.push_back(node);
                }
            }
            size = Tree.size();
            std::cout << "number of Nodes " << size << '\n';
            for (int i=0; i<size; i++) {
                std::cout << Tree[i] << " ";
            }
            std::cout<<"\n";
        }

        void getChild(char node) {
            for (int i=0; i<size-1; i++) {
                if (Tree[i] == node) {
                    std::cout << "Child of node is: " << Tree[i+1] << '\n';
                    return;
                }
            }
            std::cout<<"Node is not found" << '\n';
        }
};

int main() {
    SingleChildTree sct;
    sct.createTree();

    char nodeToFind;
    std::cout << "Which node to find: ";
    std::cin >> nodeToFind;

    sct.getChild(nodeToFind);
}
```

## Relation to Tensors

To understand how this tree structure relates to tensors, let's consider a numpy.ndarray with shape (2,2,2) of ones:

![Tensor Tree Structure](https://github.com/user-attachments/assets/b8c576a8-d2bb-4581-a99c-6f4342ec1a9c)

- The first dimension (array.shape[0] = 2) corresponds to two nodes at the first level.
- The second dimension (array.shape[1] = 2) means each node from the previous level has two child nodes, resulting in 4 nodes at the second level.
- The third dimension (array.shape[2] = 2) results in 8 leaf nodes, which contain the actual values.

### Important Note on Tensor Slicing

When we slice a tensor, we create a new tensor with a reduced dimensionality:

```python
array = np.ones((2,3,2))  # A different example
arrayAtDim1 = array[0]
assert(arrayAtDim1.shape == array.shape[1:])
```

**Task:** Explain why the shape of `arrayAtDim1` is equal to `array.shape[1:]`.

## Next Steps

We'll implement a more complex node structure to better represent tensors and their operations.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

No license yet
