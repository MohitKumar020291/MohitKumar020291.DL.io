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
