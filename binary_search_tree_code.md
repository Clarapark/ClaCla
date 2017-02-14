### Binary Search Tree

#### Implementation

```c++
#include <iostream>
#include "tree.h"
using namespace std;
int main(int argc, char* argv[]) {
  BinarySearchTree<int> bst;
  function<int(int&, int&)> comparator = [](int& lhs, int& rhs)->int{
    if(lhs > rhs) {
      return 1;
    } else if (lhs < rhs) {
      return -1;
    } else {
      return 0;
    }
  };

  function<void(int& value)> printer = [](int& value)->void{
    std::cout << value << std::endl;
  };

  bst.insert(3, comparator);
  bst.insert(2, comparator);
  bst.insert(5, comparator);
  bst.insert(4, comparator);
  bst.insert(6, comparator);

  // std::cout << bst.search(1, comparator) << std::endl;
  // bst.insert(1, comparator);
  // std::cout << bst.search(1, comparator) << std::endl;

  bst.remove(5, comparator);
  bst.traverse_pre_order(printer);

  return 0;
}
```

#### Insert

-	삽입할 값이 현재 값보다 작으면 좌측, 크면 우측으로 이동하다가 비어있는 지점에 삽입

```c++
template <typename T>
bool BinarySearchTree<T>::insert(T value, function<int(T&, T&)>& comp) {
   return internal_insert(root, value, comp);
 }
 template <typename T>
 bool BinarySearchTree<T>::internal_insert(Node<T>*& current, T value,
                                          function<int(T&, T&)>& comp) {
  // recursive
  if (current == nullptr) {
    current = new Node<T>(value);
    return true;
  } else if (comp(current->data, value) == 1) {
    // if the variable current is greater than value,
    return internal_insert(current->left, value, comp);
  } else if (comp(current->data, value) == -1) {
    // if the variable current is less than value,
    return internal_insert(current->right, value, comp);
  }

  // duplicated
  return false;
}
```

#### Traverse

-	중위순회, 전위순회, 후위순회를 공부하기 좋은 코드, f는 cout 이라 봐도 됨

```c++
template <typename T>
void BinarySearchTree<T>::traverse_pre_order(function<void(T&)>& printer) {
  // depth-first traversal
  internal_traverse_pre_order(root, printer);
}

template <typename T>
void BinarySearchTree<T>::internal_traverse_pre_order(Node<T>* current, function<void(T&)>& f) {
  if (current == nullptr) {
    return;
  }
  f(current->data);
  internal_traverse_pre_order(current->left, f);
  internal_traverse_pre_order(current->right, f);
}

template <typename T>
void BinarySearchTree<T>::traverse_in_order(function<void(T&)>& printer) {
   // depth-first traversal
   internal_traverse_in_order(root, printer);
 }

 template <typename T>
 void BinarySearchTree<T>::internal_traverse_in_order(Node<T>* current, function<void(T&)>& f) {
   if (current == nullptr) {
     return;
   }

   internal_traverse_in_order(current->left, f);
   f(current->data);
   internal_traverse_in_order(current->right, f);
 }

 template <typename T>
 void BinarySearchTree<T>::traverse_post_order(function<void(T&)>& printer) {
   // depth-first traversal
   internal_traverse_post_order(root, printer);
 }

 template <typename T>
 void BinarySearchTree<T>::internal_traverse_post_order(Node<T>* current, function<void(T&)>& f) {
   if (current == nullptr) {
     return;
   }

   internal_traverse_post_order(current->left, f);
   internal_traverse_post_order(current->right, f);
   f(current->data); }
```

#### Remove

```c++
template <typename T>
Node<T>*& BinarySearchTree<T>::find_left_most_child(Node<T>*& current) {

   while(current->left) {
     current = current->left;
   }

   return current;
 }

 template <typename T>
 void BinarySearchTree<T>::replace_node(Node<T>*& replaced, Node<T>*& newone) {
   if (replaced == nullptr || newone == nullptr) {
     return;
   }

   if (replaced->left != nullptr && replaced->right != nullptr) {
      newone->left = replaced->left;
      if(replaced->right != newone) {
        newone->right = replaced->right;
      }
    }

    Node<T>* temp = replaced;
    replaced = newone;
    delete temp;

    return;
  }

  template <typename T>
  bool BinarySearchTree<T>::remove(T value, function<int(T&, T&)>& comp) {
    return internal_remove(root, value, comp);
  }

  template <typename T>
  bool BinarySearchTree<T>::internal_remove(Node<T>*& current, T value, function<int(T&, T&)>& comp) {
    if (comp(current->data, value) == 0) {
      if (current->left == nullptr && current->right == nullptr) {
        // if leaf node,
        delete current;
        current = nullptr;
      } else if (current->left != nullptr && current->right != nullptr) {
        // if has two children
        replace_node(current, find_left_most_child(current->right));
      } else if (current->left != nullptr && current->right == nullptr) {
        // only has a left child;
        replace_node(current, current->left);
      } else if (current->left == nullptr && current->right != nullptr) {
        // only has a right child
        replace_node(current, current->right);
      }

      return true;
    } else if (comp(value, current->data) == 1) {
      // if the variable value is greater than current node's data
      return internal_remove(current->right, value, comp);
    } else {
      // if the variable value is less than current node's data
      return internal_remove(current->left, value, comp);
    }

    return false;
  }
```

#### Search

```c++
template <typename T>
bool BinarySearchTree<T>::search(T value, function<int(T&, T&)>& comp) {
   Node<T>* current = root;

  while (current) {
    if (comp(current->data, value) == 0) {
      return true;
    } else if (comp(value, current->data) == 1) {
      current = current->right;
    } else {
      current = current->left;
    }
  }

  return false;
}
```

*comp()는 두 값 같으면 0, 좌측이 크면 1, 우측이 크면 -1 리턴*
