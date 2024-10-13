#### _In this section we are going to create tensors from scratch, the backend is written into cpp, and the wrappers api are written into python, the try is using yaml to invoke backend using python instead using pybind11_
  - Basic tree to tensors approach:
      * What are tensors? They are just arrays/vectors with more than two axis.
      * A general tree architecture using normal list
           
        ```
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
     
        This is a simple tree implementation, each value here is a node, and they have child nodes. How it is related to tensors? Say we have numpy.ndarray with shape (2,2,2) of ones. What does it means in general is, we have a tree which looks like:
           
        ![image](https://github.com/user-attachments/assets/b8c576a8-d2bb-4581-a99c-6f4342ec1a9c)
    
    What is happening is the first dimenson of that array, array.shape[0] is,  2. So, the head node, must have two nodes, the total nodes till dim 1 are 2. Now the second dimension of that array, array.shape[1], 2, so, each node of previous dim must have two nodes, so, the total number of nodes at dim 2 are 2 * 2 = 4. Similarly the third dim will have 2 nodes, means the node at dim 3 are 4 * 2 = 8. Which are real values of node, and they themselves have empty shape. But all above them have shape whole length is > 0. i.e.
```
array = np.ones((2,3,2)) #a different example
arrayAtDim1 = array[0]
assert(arrayAtDim1.shape == shape[1:])
```

We simply picked up the left node to the head, a new head is created which hypothetically stored into `arrayAtDim1`. Task: answer why the shape of `arrayAtDim1` is equal to `array.shape[1:]`.


Let's just implement the simple node structure.
