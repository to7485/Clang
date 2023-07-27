# 트리
- 나무를 닮은 자료구조이다.
- 기업에서 전략을 수립할 대 사용하는 의사결정 트리, 게임에서 사용하는 스킬트가 예이다.
- 운영체제의 파일 시스템이 트리 구조로 이루어져 있고, HTML이나 XML문서를 다룰 때 사용하는 DOM도 트리구조로 이루어져 있다.

## 트리의 구성 요소
- 트리는 뿌리(Root),가지(Branch),잎(leaf)세 가지 요소로 이루어져 있다.

![image](https://github.com/to7485/Clang/assets/54658614/d84b5313-1a80-4bc0-89dc-9e50dca0b22d)

- 뿌리, 가지, 잎은 근본적으로는 똑같은 노드이다.
- 트리에서 어디에 위치하는가에 따라 불리는 이름이 달라진다.
- 뿌리(Root)는 트리 자료구조의 가장 위에 있는 노드를 가리킨다.
- 가지(Branch)는 뿌리와 잎 사이에 있는 모든 노드를 일컫는다.
- 잎(Leaf)는 가지의 끝에 매달린 노드이다.(잎 노드는 단말노드 라고 부르기도 한다.)

## 트리의 각 구성요소의 명칭과 관계

![image](https://github.com/to7485/Clang/assets/54658614/87dea319-f51d-440b-9a6f-24c1135047dd)

- B에서 C,D가 뻗어나와 있다.
- 이때 B는 C와 D의 부모이고, C와 D는 B의 자식이다.
- 한 부모 밑에서 태어난 C와 D를 형제라고 한다.

### 노드의 경로
- 한 노드에서 다른 한 노드까지 이르는 길 사이에 있는 노드들의 순서를 경로라고 한다.

![image](https://github.com/to7485/Clang/assets/54658614/58f7a2b3-6d87-4854-a6c0-c1f53b60a27c)

- B에서 F로 갈때의 경로는 'B D F'가 된다.

### 노드의 길이
- 출발 노드에서 목적지 노드까지 거쳐가야 하는 노드의 개수
- B D F의 경로의 길이는 2가 된다.

### 노드의 깊이
- 뿌리 노드에서 목표 노드까지 이르는 경로의 길이.

![image](https://github.com/to7485/Clang/assets/54658614/f03b7cfc-a428-49a0-8459-7ef6f245f486)

- K 노드는 A노드로부터 이어지는 경로의 길이가 3이므로 깊이 또한 3이다.

### 노드의 레벨
- 깊이가 같은 노드들의 집합을 일컫는말이다.
- 레벨2 라고 하면 C D H J 노드 전체를 가리킨다.

### 노드의 높이
- 가장 깊은 곳에 있는 잎 노드까지의 길이
- 위 그림에서 높이는 3이 된다.

### 노드의 차수, 트리의 차수

![image](https://github.com/to7485/Clang/assets/54658614/a9f8289a-d1ac-427a-8928-ef2b45118b18)

- 노드의 차수는 한 노드의 자식 노드의 개수
- 트리의 차수는 트리 내에 있는 노드들 가운데 자식 노드가 가장 많은 노드의 차수를 말한다.

## 트리의 표현방법

### 중첩된 괄호 표현법
- 같은 레벨의 노드들을 괄호로 묶어서 표현하는 방법

![image](https://github.com/to7485/Clang/assets/54658614/e9272b76-4c54-4da9-a82b-a9bbd385c7e4)

### 중첩된 집합
- 트리가 하위 트리의 집합이라는 사실을 잘 표현할 수 있다는 장점이 있다.

![image](https://github.com/to7485/Clang/assets/54658614/4af87a64-c234-4526-84f6-aef755d0b4ee)

### 들여쓰기 표현
- 들여쓰기로 표현한 트리는 자료의 계층적인 특징을 잘 나타낸다.
- 윈도우 탐색기의 폴더 트리가 들여쓰기로 표현한 좋은 예이다.

![image](https://github.com/to7485/Clang/assets/54658614/0404e6e9-9ace-4582-b472-f9b8eb25fe56)


## 트리의 연산

## 노드의 표현
- 왼쪽 자식 - 오른쪽 형제 표현법
- 왼쪽 자식과 오른쪽 형제에 대한 포인터만을 갖도록 노드를 구성하는 방법이다.
- 이 표현법을 사용하면 n개의 차수를 가진 노드의 표현이 오로지 2개의 포인터(왼쪽 자식 포인터와 오른쪽 형제포인터)만으로 가능하게 된다.

![image](https://github.com/to7485/Clang/assets/54658614/2e0fde86-5171-471f-97ba-0d7ce3a704b7)


![image](https://github.com/to7485/Clang/assets/54658614/8041b1b8-98b1-43d5-9ea9-d6eb38c31512)

## 노드 선언
- 데이터를 담는 Data필드, 왼쪽자식과 오른쪽 형제를 가리키는 2개의 포인터로 구성된다.
```c
typedef char ElementType;

typedef struct tagLCRSNode 
{
    struct tagLCRSNode* LeftChild;
    struct tagLCRSNode* RightSibling;

    ElementType Data;
} LCRSNode;
```

## 노드 생성/소멸 연산

### 노드의 생성
- malloc()함수를 이용하여 LCRSNode 구조체의 크기만큼 Heap 영역에 메모리를 할당하고
- 매개변수 NewData를 Data에 저장한 후 노드의 메모리 주소를 반환한다.
```c
LCRSNode* LCRS_CreateNode( ElementType NewData )
{
    LCRSNode* NewNode = (LCRSNode*)malloc( sizeof(LCRSNode) );
    NewNode->LeftChild    = NULL;
    NewNode->RightSibling = NULL;
    NewNode->Data = NewData;

    return NewNode;
}
```

### 노드의 소멸
```c
void LCRS_DestroyNode( LCRSNode* Node )
{
    free(Node);
}
```

## 자식노드 연결
- 부모노드와 이 부모노드에 연결할 자식 노드를 매개 변수로 받는다.
- 먼저 부모 노드인 Parent에게 자식 노드가 있는지 검사한다.
- LeftChild가 NULL인것을 확인하면 자식이 하나도 없다는 사실 정도 알 수 있다.
- Parent의 LeftChild 포인터에 자식 노드의 주소를 저장하면 된다.

![image](https://github.com/to7485/Clang/assets/54658614/fca889fc-e633-41e5-8139-4865275a5d5a)

- Parent의 LeftChild가 NULL이 아닌 경우 자식 노드를 하나 이상 갖고 있다는 의미이다.
- 이럴때 자식 노드의 RightSibling 포인터를 이용해 가장 오른쪽에 있는 자식 노드(RightSibling이 NULL인 노드)를 찾아낸다.
- 이렇게 찾아낸 가장 오른쪽 자식 노드의 RightSibling에 대해 Child를 대입한다.
- 이렇게 하면 Parent는 새로운 자식을 하나 더 얻게 된다.

![image](https://github.com/to7485/Clang/assets/54658614/409255e8-518f-4ce9-8382-eab7c2c2f969)

```c
void LCRS_AddChildNode( LCRSNode* Parent, LCRSNode *Child)
{
    if ( Parent->LeftChild == NULL )
    {
        Parent->LeftChild = Child;
    }
    else 
    {
        LCRSNode* TempNode = Parent->LeftChild;
        while ( TempNode->RightSibling != NULL )
            TempNode = TempNode->RightSibling;

        TempNode->RightSibling = Child;        
    }
}
```
## 트리의 소멸
```c
void LCRS_DestroyTree( LCRSNode* Root )
{
    if ( Root->RightSibling != NULL )
        LCRS_DestroyTree( Root->RightSibling );

    if ( Root->LeftChild != NULL )
        LCRS_DestroyTree( Root->LeftChild );

    Root->LeftChild = NULL;
    Root->RightSibling = NULL;

    LCRS_DestroyNode( Root );
}
```

## 트리의 출력
- 깊이-1 만큼 공백을 3칸씩 출력한다.
- 공백의 마지막에는 해돵 노드가 누군가의 자식 노드임을 나타내는 '+--'를 덧붙인 후 노드의 데이터를 출력한다.
- 이렇게 하면 깊이가 0인 뿌리 노드는 제일 앞쪽에 출력되고 잎 노드는 제일 뒤쪽에 출력된다.

```c
void LCRS_PrintTree( LCRSNode* Node, int Depth )
{
    // 들여쓰기
    int i=0; 
    for ( i=0; i<Depth-1; i++ )
        printf("   "); // 공백 3칸

    if (Depth > 0) // 자식 노드 여부 표시
        printf("+--");
    
    // 노드 데이터 출력
    printf("%c\n", Node->Data); 

    if ( Node->LeftChild != NULL )
        LCRS_PrintTree(Node->LeftChild, Depth+1);

    if ( Node->RightSibling != NULL )
        LCRS_PrintTree(Node->RightSibling, Depth);
}
```

## 트리 예제 프로그램
```c
int main( void )
{
    //  노드 생성 
    LCRSNode* Root = LCRS_CreateNode('A');
    
    LCRSNode* B = LCRS_CreateNode('B');
    LCRSNode* C = LCRS_CreateNode('C');
    LCRSNode* D = LCRS_CreateNode('D');
    LCRSNode* E = LCRS_CreateNode('E');
    LCRSNode* F = LCRS_CreateNode('F');
    LCRSNode* G = LCRS_CreateNode('G');
    LCRSNode* H = LCRS_CreateNode('H');
    LCRSNode* I = LCRS_CreateNode('I');
    LCRSNode* J = LCRS_CreateNode('J');
    LCRSNode* K = LCRS_CreateNode('K');

    //  트리에 노드 추가 
    LCRS_AddChildNode( Root, B );
        LCRS_AddChildNode( B, C );
        LCRS_AddChildNode( B, D );
            LCRS_AddChildNode( D, E );
            LCRS_AddChildNode( D, F );

    LCRS_AddChildNode( Root, G );
        LCRS_AddChildNode( G, H );

    LCRS_AddChildNode( Root, I );
        LCRS_AddChildNode( I, J );
            LCRS_AddChildNode( J, K );
    
    //  트리 출력 
    LCRS_PrintTree( Root, 0 );

    //  트리 소멸시키기 
    LCRS_DestroyTree( Root );

    return 0;
}
```






