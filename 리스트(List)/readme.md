# 자료구조
- 자료구조(Data Structure)는 컴퓨터가 데이터를 효율적으로 다룰 수 있게 도와주는 <b>데이터 보관 방법과 데이터에 관한 연산의 총체</b>를 뜻한다.
- 예를들어 int도 자료구조이다. int는 32bit 메모리 공간 안에 수를 할당하되 첫 비트를 부호 표현에 사용하는 등의 '보관방법'을 정의하고 있고, 덧셈/뺄셈/나눗셈/곱셈/논리/시프트등 다양한 '연산' 또한 정의하고 있다.

## 자료구조의 종류
- 단순 자료구조
    - 프로그래밍 언어에서 통상적으로 제공하는 기본 데이터 형식을 말한다.
- 복합 자료구조
    - 선형 자료구조
        - 데이터 요소를 순차적으로 연결하는 자료구조로, 구현하기 쉽고 사용하기도 쉽다.
        - 배열(Array),링크드 리스트(Linked List), 스택(Stack), 큐(Queue)가 있다.
     
![image](https://github.com/to7485/Clang/assets/54658614/8b2196ea-1d7d-49b2-9115-8af434f878bf)

    - 비선형 자료구조
        - 데이터를 비 순차적으로 연결한다.
        - 한 데이터 요소에서 여러 데이터 요소로 연결되기도 하고, 여러 데이터 요소에서 하나의 데이터 요소로 연결되기도 한다.
        - 트리(Tree),그래프(Graph)가 있다.


![image](https://github.com/to7485/Clang/assets/54658614/2093684c-d9ea-4393-8d87-b1ddbb7ba8a2)

- 자료구조의 종류

![image](https://github.com/to7485/Clang/assets/54658614/c53b4c80-8f11-4361-928c-010198c78227)

## ADT(Abstract Data Types)
- 추상 데이터 형식
- 자료구조의 동작 방법을 표현하는 데이터형식입니다.
- 예를들어 조회하거나 추가하거나 삭제하거나 하는등의 일련의 기능들이 있다.
- C언어로 표현하면 함수가 된다.

## 자료구조를 공부해야 하는 이유
1. 라이브러리에서 엉뚱한 자료구조를 선택하는 일을 피할 수 있다.
2. 데이터를 효율적으로 사용할 수 있게 도와주는 핵심 부품 역할을 한다.

# 알고리즘
- 알고리즘(Algorithm)은 9세기 페르시아 수학자 알 콰리즈미의 이름에서 유래된 말이다.
- 어떤 문제를 풀기 위한 절차를 뜻한다.
- 알고리즘을 설계한다는 것은 문제 풀이 절차를 설계한다는 의미이다.
- 알고리즘을 구현한다는 것은 프로그래밍 언어를 이용해 문제 풀이 절차를 실제로 동작하는 코드로 작성한다는 의미이다.

![image](https://github.com/to7485/Clang/assets/54658614/69f7dfe8-003b-4cfa-94a0-d26f8388dc9e)

# 포인터의 복습
- 포인터 변수의 선언
```c
//자료형* 포인터변수명;
int* ptr;
```
- 주소연산자를 통해 다른 변수의 주소를 할당할 수 있다.
```c
int a = 123;
int* ptr = &a;
```



# 리스트(List)
- 리스트란 순서를 가진 항목들의 모임이다
- 데이터를 나란히 저장한다.
- 중복된 데이터의 저장을 허용한다.

## 노드(Node)
- 리스트의 목록을 이루는 개별의 요소를 노드라고 칭한다.
- 이 노드(Node)라는 개념은 스택, 큐, 트리를 하면서 계속 사용하게될 개념이다.
- 리스트에서 첫번째 Node는 Head, 마지막 Node는 Tail이라고 부릅니다.
  
![image](https://github.com/to7485/Clang/assets/54658614/f1e96cff-2e92-478b-b805-10e6bb00ad73)

## 리스트와 배열의 비교

### 배열
- 배열은 리스트처럼 데이터 목록을 다루며, C언어에서 기본적으로 제공하기 때문에 프로그래머가 따로 구현하지 않아도 된다.
- 하지만 배열은 생성하는 시점에 반드시 배열의 크기를 지정해야 하고 생성한 후에는 크기를 변경할 수 없다.
- 소프트웨어는 종종 프로그래머에게 배열의 한계를 넘어설 것을 요구하고 있다.
- 예를들어 임의의 폴더 안에있는 파일 목록을 필요로 할 때 폴더 안에 하나도 없을 수도 있고, 수천, 수만개의 파일이 있을 수도 있다.

### 리스트
- 배열처럼 집합 보관 기능을 가지면서도 배열과 달리 유연하게 크기를 바꿀 수 있는 자료구조이다.
- 간단하면서도 활용도가 높고 스택,큐,트리와 같은 자료구조를 이해할 수 있는 기반이 된다는 점에서 중요한 의미를 가진다.
- 링크드 리스트, 더블 링크드 리스트, 환형 링크드 리스트 등이 있다.


## 링크드 리스트(Linked List)
- 링크드 리스트는 리스트를 구현하는 여러 가지 기법 중에서도 가장 간단한 방법이다.
- 링크드 리스트는 <b>노드를 연결해서 만든 리스트</b>이다.

### 링크드 리스트의 노드
- 링크드 리스트의 노드는 데이터를 보관하는 필드, 다음 노드와 연결고리 역할을 하는 포인터로 이루어진다.

![image](https://github.com/to7485/Clang/assets/54658614/788fd02b-a6d2-4b1f-b97b-612d1702a1fd)

- 데이터와 포인터로 이루어진 노드들을 다음과 같이 모두 엮으면 링크드 리스트가 되는것이다.

![image](https://github.com/to7485/Clang/assets/54658614/add701e4-0e6a-4879-89f7-a01715cb1d5a)

### 링크드 리스트의 노드 표현
- 링크드 리스트의 노드를 C언어료 표현하면 다음과 같은 구조체로 나타낼 수 있다.
- ElementType을 int로 정했지만, 나중에 각자 필요한 자료형으로 바꿔서 사용하면 된다.
```c
typedef int ElementType;

typedef struct{
	ElementType Data; //데이터
	struct Node* NextNode;//다음노드
}Node;

void main() {
    //이렇게 선언한 Node구조체로 간편하게 인스턴스를 만들 수 있다.
	Node myNode;
}
```

### 링크드 리스트의 주요 연산
- 링크드 리스트에는 두 종류의 연산이 필요하다.
    1. 자료구조를 구축하기 위한 연산
    2. 자료구조에 저장된 데이터를 활용하기 위한 연산

- 링크드 리스트 자료구조의 여섯가지 주요 연산
    - 노드 생성(CreateNode)/소멸(DestoryNode)
    - 노드 추가(AppendNode)
    - 노드 탐색(GetNodeAt)
    - 노드 삭제(RemoveNode)
    - 노드 삽입(InsertAfter, InsertNewHead)

### 노드 생성/소멸 연산
- 노드는 Heap 영역에 생성해서 우리가 원할 때 메모리를 할당받고 원할 때 소멸시켜야 한다.
```c
Node* SLL_CreateNode(ElementType NewData) {
	Node* NewNode = (Node*)malloc(sizeof(Node));
	//malloc()은 메모리를 할당해주고 그 주소를 void*형으로 반환한다.
	//그렇기 때문에 Node형으로 형변환을 해줘야 한다.

	NewNode->Data = NewData; //데이터를 저장한다.
	NewNode->NextNode = NULL;
}
```
- 노드가 존재하는 주소를 가리키는 포인터를 입력받아 free()함수에 넘겨 해당 노드를 소멸시킨다.

```c
void SLL_DestoryNode(Node* Node) {
	free(Node);
}
```

### 노드 추가 연산
- 노드 추가는 링크드 리스트의 Tail Node 뒤에 새로운 Node를 만들어 연결하는 연산이다.
- 꼬리를 덧붙히는 모양

![image](https://github.com/to7485/Clang/assets/54658614/2b1433ec-bd0e-4e6a-b6ea-fd2a7ee52340)

- Heap영역에 SLL_CreateNode()함수를 이용하여 Node한개를 생성한다음,
-  생성한 노드의 주소를 Tail의 NextNode의 포인터에 저장해주자.

```c
void SLL_AppendNode(Node** _Head, Node* _NewNode) {
	//Head Node가 NULL이라면 새로운 Node가 Head가 된다.
	if ((*Head) == NULL) {
		*Head = NewNode;
	}
	else {
		//Tail을 찾아 NewNode에 연결한다.
		Node* Tail = (*Head);
		while (Tail->NextNode != NULL) {
			Tail = Tail->NextNode;
		}
		Tail->NextNode = NewNode;
	}
}
```
#### 더블포인터 **를 써야하는 이유
- SLL_Append()함수를 호출할 때 SLL_AppendNode()의 매개변수들은 지역변수이기 때문에 Stack영역에 만들어진다.
- List는 _Head에, NewNode는 _NewNode에 자신이 가리키는 주소를 '복사'해 넣습니다.
- 싱글포인터를 사용하게 되면 SLL_AppendNode()함수를 호출할 때 List포인터가 담고 있는 '주소값'만 _Head에 복사가 된다.
- 정작 List 포인터 변수의 주소는 전달이 되지 않는 상황이 된다.
- 그렇기 때문에 SLL_AppendNode()함수가 호출된 후 매개변수 _Head와 _Node는 소멸되기 때문에 List는 그냥 NULL로 남아있게 된다.
- 포인터가 가진 값이 아닌 포인터 자신의 주소를 넘겨야 하는 것이다.


- main에서 다음과 같이 사용한다.
```c
void main() {
	Node* List = NULL;
	Node* NewNode = NULL;
	NewNode = SLL_CreateNode(117); //Heap영역에 Node 생성
	SLL_AppendNode(&List, NewNode);//생성한 Node를 List에 추가
	NewNode = SLL_CreateNode(119);//Heap영역에 또 다른 Node 생성
	SLL_AppendNode(&List, NewNode);//생성한 Node를 List에 추가
}
```
### 노드 탐색 연산
- 배열에서는 어떤 위치에 있는 요소를 취하고 싶을 때 해당 요소의 첨자를 입력하면 바로 해당 요소에 접근할 수 있다.
- 이에 반해 링크드 리스트는 헤드부터 시작해서 다음 노드에 대한 포인터를 징검다리 삼아 차근차근 노드의 개수만큼 거쳐야만 원하는 요소에 접근할 수 있다.
- 찾고자 하는요소가 N번째에 있다면 N-1개의 노드를 거쳐야 한다는 것이다.

```c
Node* SLL_GetNodeAt(Node* Head, int Location) {
	Node* Current = Head; //Current에 Head를 대입한다.
	while (Current != NULL && (--Location) >= 0) {
		Current = Current->NextNode; //NextNode의 주소값을 넣어준다.
	}
	return Current;
}
```
- 이 함수는 다음과 같이 사용할 수 있다.

```c
void main() {
	Node* List = NULL;
	Node* NewNode = NULL;
	Node* MyNode = NULL;
	NewNode = SLL_CreateNode(117); //Heap영역에 Node 생성
	SLL_AppendNode(&List, NewNode);//생성한 Node를 List에 추가
	NewNode = SLL_CreateNode(119);//Heap영역에 또 다른 Node 생성
	SLL_AppendNode(&List, NewNode);//생성한 Node를 List에 추가

	MyNode = SLL_GetNodeAt(List, 1); //두 번째 노드의 주소를 MyNode에 저장
	printf("%d\n", MyNode->Data); //119를 출력
}
```

### 노드 삭제 연산
- 링크드 리스트 내 임의의 노드를 제거하는 연산이다.
- 삭제하고자 하는 노드를 찾은 후 해당 노드의 다음 노드를 이전 노드의 NextNode 포인터에 연결하면 그 노드를 삭제할 수 있다.

![image](https://github.com/to7485/Clang/assets/54658614/77c6d792-01da-4891-8863-aa4a771b1329)

```c
void SLL_RemoveNode(Node** Head, Node* Remove) {
	if (*Head == Remove) {
		*Head == Remove->NextNode;
	}
	else {
		Node* Current = *Head;
		while (Current != NULL && Current->NextNode != Remove) {
			Current = Current->NextNode;
		}
		if (Current != NULL) {
			Current->NextNode = Remove->NextNode;
		}
	}
}
```

- 노드를 삭제해보자.

```c
void main() {
	Node* List = NULL;
	Node* NewNode = NULL;
	Node* MyNode = NULL;
	NewNode = SLL_CreateNode(117); //Heap영역에 Node 생성
	SLL_AppendNode(&List, NewNode);//생성한 Node를 List에 추가
	NewNode = SLL_CreateNode(119);//Heap영역에 또 다른 Node 생성
	SLL_AppendNode(&List, NewNode);//생성한 Node를 List에 추가

	MyNode = SLL_GetNodeAt(List, 1); //두 번째 노드의 주소를 MyNode에 저장
	printf("%d\n", MyNode->Data); //119를 출력

	NewNode = SLL_CreateNode(212);//Heap영역에 또 다른 Node 생성
	SLL_AppendNode(&List, NewNode);//생성한 Node를 List에 추가

	SLL_RemoveNode(&List, MyNode); //두 번째 노드 제거
	SLL_DestoryNode(MyNode); //링크드 리스트에서 제거한 노드를 메모리에서 완전히 소멸시킴
}
```

### 노드 삽입 연산
- 노드와 노드 사이에 새로운 노드를 끼워넣는 연산

![image](https://github.com/to7485/Clang/assets/54658614/d595a7fc-8437-428e-9abd-862202f9b86a)

```c
void SSL_InsertAfter(Node* Current, Node* NewNode) {
	NewNode->NextNode = Current->NextNode;
	Current->NextNode = NewNode;
}
```

### 정리코드
```c
void main() {
	Node* List = NULL;
	Node* NewNode = NULL;
	Node* MyNode = NULL;
	Node* Current = NULL;
	int Count = 0;

	NewNode = SLL_CreateNode(117); //Heap영역에 Node 생성
	SLL_AppendNode(&List, NewNode);//생성한 Node를 List에 추가
	NewNode = SLL_CreateNode(119);//Heap영역에 또 다른 Node 생성
	SLL_AppendNode(&List, NewNode);//생성한 Node를 List에 추가


	MyNode = SLL_GetNodeAt(List, 1); //두 번째 노드의 주소를 MyNode에 저장
	
	Count = SLL_GetNodeCount(List);//리스트의 개수 저장

	for (int i = 0; i < Count; i++) {
		Current = SLL_GetNodeAt(List, i);
		printf("List[%d] : %d\n", i, Current->Data);
	}

	NewNode = SLL_CreateNode(212);//Heap영역에 또 다른 Node 생성
	SLL_AppendNode(&List, NewNode);//생성한 Node를 List에 추가

	SLL_RemoveNode(&List, MyNode); //두 번째 노드 제거
	SLL_DestoryNode(MyNode); //링크드 리스트에서 제거한 노드를 메모리에서 완전히 소멸시킴

	MyNode = SLL_GetNodeAt(List, 1); //두 번째 노드의 주소를 MyNode에 저장

	Current = SLL_GetNodeAt(List, 0);
	NewNode = SLL_CreateNode(3000);

	SLL_InsertAfter(Current, NewNode);

	//리스트의 출력
	Count = SLL_GetNodeCount(List);
	for (int i = 0; i < Count; i++) {
		Current = SLL_GetNodeAt(List, i);
		printf("List[%d] : %d\n", i, Current->Data);
	}

}
```















