Tree
====

### Tree?

![](image/Tree1.png)

-	계층적 구조(비선형 구조)를 띄고 있는 자료구조
-	주된 목적 => **탐색**
-	의사결정, 파일 시스템(디렉토리 구조), 검색 엔진, DBMS, 라우터 알고리즘, 계층적 데이터를 다루는 등 매우 다양한 곳에서 응용

| 용어         | 설명                                                                       |
|--------------|----------------------------------------------------------------------------|
| 차수(degree) | 어떤 노드가 가지고 있는 자식 노드의 수 (예 : A 노트 차수 2, B 노드 차수 2) |
| 레벨(level)  | 트리의 각 층의 번호 (예 : 레벨 1은 A, 레벨 2는 B)                          |
| 높이(height) | 트리의 루트 노드부터 시작하여 맨 끝에있는 잎 노드까지의 깊이 (예 : 깊이 3) |

### Binary Tree

-	노드는 최대 2개의 자식 노드를 가질 수 있는 자료구조
-	이진트리에는 여러 형태가 존재

**Complete Binary Tree**

![](image/complete_binarytree.png)

-	어떤 잎 노드 두개의 레벨차가 1 이하이며, 왼쪽부터 오른쪽으로 채워지는 트리

**Skewed Binary Tree**

![](image/skewed_binarytree.png)

-	루트 노드를 제외한 모든 노드가 부모 노드의 왼쪽 자식노드이거나 혹은 오른쪽 자식 노드인 트리
-	즉 노드 방향이 한쪽 방향으로만 치우쳐져 있음

**Full Binary Tree**

![](image/Full_binarytree.png)

-	최대한 노드가 가득차있는 트리
-	모든 노드가 자식 노드를 2개나 가지고 있다
-	모든 포화 이진 트리는 완전이진 트리 (역은 성립하지 않는다)

### Tree Traversal

**Preorder Traversal**

![](image/preorder_traversal.png)

-	루트 노드를 시작으로 아래로 내려오며 좌측 하위트리를 먼저 방문하고, 방문이 끝나면 우측 하위 트리를 방문

**Inorder Traversal**

![](image/inorder_traversal.png)

-	좌측 하위 트리부터 시작하여 루트 노드를 거치고 우측 하위 트리를 방문

**Postorder Traversal**

![](image/postorder_traversal.png)

-	좌측 하위 트리부터 시작하여 우측 하위트리를 거치고 마지막으로 루트 노드를 방문

**Levelorder Traversal**

![](image/levelorder_traversal.png)

-	루트 노드부터 시작하여 레벨 순서대로 차례로 각각 방문
-	A -> B -> C -> D -> E -> F -> G -> H

**스택을 이용하지 않는 순회**

-
