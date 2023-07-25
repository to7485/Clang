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
void SLL_AppendNode(Node** Head, Node* NewNode) {
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

	//모든 노드를 메모리에서 제거
	for (int i = 0; i < Count; i++) {
		Current = SLL_GetNodeAt(List, 0);
		if (Current != NULL) {
			SLL_RemoveNode(&List, Current);
			SLL_DestoryNode(Current);
		}
	}

}
```

## 링크드 리스트의 장점
- 배열보다 새로운 노드의 추가,삽입,삭제가 쉽고 빠르다.

## 링크드 리스트의 단점
- 특정 위치에 있는 노드에 접근하는 연산은 느리다.


# 더블 링크드 리스트(Double Linked List)
- LinkedList의 탐색 기능을 개선한 자료구조이다.
- LinkedList에서 어떤 노드를 찾으려면 Head에서 Tail방향으로만 탐색할 수 있다.
- Double Linked List에서는 양방향 탐색이 가능하다.
- 양방향 탐색이 가능한 이유는 리스트를 구성하는 Node의 구조가 변경되었기 때문이다.
- Double Linked List의 Node는 자신의 앞에있는 Node를 가리키는 포인터도 갖고 있습니다.
- 그래서 Double Linked List의 Node는 앞뒤로 이동할 수 있다.

![image](https://github.com/to7485/Clang/assets/54658614/4604c261-e4f8-4c9d-801e-3565c03a4511)

## Node의 구성
- Double Linked List의 Node의 구성은 다음과 같다.
```c
typedef int ElementType;

typedef struct tagNode {
	ElementType Data;
	struct tagNode* PrevNode;
	struct tagNode* NextNode;
}Node;
```

![image](https://github.com/to7485/Clang/assets/54658614/206a0180-837c-4730-9de6-ca67289c496c)


## Node의 생성/소멸
```c
//노드의 생성
Node* DLL_CreateNode(ElementType NewData) {
	Node* NewNode = (Node*)malloc(sizeof(Node));

	NewNode->Data = NewData;
	NewNode->PrevNode = NULL;
	NewNode->NextNode = NULL;

	return NewNode;
}
```
- 노드의 소멸
- 링크드리스트와 동일하게 free()함수를 호출한다.
```c
//노드의 소멸
void DLL_DestoryNode(Node* Node) {
	free(Node);
}
```

## 노드의 추가연산
- Double Linked List에서는 새로운 Tail의 PrevNode 포인터도 기존 Tail의 주소를 가리키도록 해야 한다.

![image](https://github.com/to7485/Clang/assets/54658614/e8a1b649-75ad-4e1f-b820-b006fc6882e9)

```c
//노드의 추가
void DLL_AppendNode(Node** Head, Node* NewNode) {
	//헤드 노드가 NULL이라면 새로운 노드가 Head가 된다.
	if ((*Head) == NULL) {
		*Head = NewNode;
	}
	else {
		//테일을 찾아 NewNode를 연결한다.
		Node* Tail = (*Head);
		while (Tail->NextNode != NULL) {
			Tail = Tail->NextNode;
		}

		Tail->NextNode = NewNode;
		NewNode->PrevNode = Tail;//기존의 Tail을 새로운 Tail의 PrevNode가 가리킴
	}
}
```

## 노드의 탐색
```c
//노드 탐색
Node* DLL_GetNodeAt(Node* Head, int Location) {
	Node* Current = Head;
	while (Current != NULL && (--Location) >= 0) {
		Current = Current->NextNode;
	}
	return Current;
}
```

## 노드 삭제 연산
- 삭제할 노드의 양쪽 포인터 2개, 이전노드의 NextNode 포인터, 다음노드의 PrevNode 포인터 4개의 포인터를 다뤄야 한다.

![image](https://github.com/to7485/Clang/assets/54658614/13d18bb4-deae-4669-bf72-6dd09f5b8fdf)

```c
//노드의 삭제
void DLL_RemoveNode(Node** Head, Node* Remove) {
	if (*Head == Remove) {
		*Head = Remove->NextNode;
		if ((*Head) != NULL) {
			(*Head)->PrevNode = NULL;
		}
		Remove->PrevNode = NULL;
		Remove->NextNode = NULL;
	}
	else {
		Node* Temp = Remove;

		if (Remove->PrevNode != NULL) {
			Remove->PrevNode->NextNode = Temp->NextNode;
		}
		if (Remove->NextNode != NULL) {
			Remove->NextNode->PrevNode = Temp->PrevNode;
		}

		Remove->PrevNode = NULL;
		Remove->NextNode = NULL;
	}
}
```

## 노드 삽입
- 새로운 노드를 삽입할 때 PrevNode 포인터로는 이전 노드를, NextNode 포인터로는 다음 노드를 가리키게 합니다.
- 그리고 이전 노드의 NextNode포인터와 다음 노드의 PrevNode포인터는 새 노드를 가리키게 합니다.

![image](https://github.com/to7485/Clang/assets/54658614/7a110308-4090-42b6-94bf-93bb2c313965)

```c
//노드 삽입
void DLL_InsertAfter(Node* Current, Node* NewNode) {
	//새 노드의 다음포인터를 현재노드의 다음포인터에 연결
	NewNode->NextNode = Current->NextNode;
	//새 노드의 이전포인터를 현재 노드를 가리키게 연결
	NewNode->PrevNode = Current;

	if (Current->NextNode != NULL) {
		Current->NextNode->PrevNode = NewNode;
		//Current->NextNode->PrevNode(다음노드의 이전포인터)
		Current->NextNode = NewNode;
	}
}
```

## 노드 개수세기 연산
```c
//노드 개수
int DLL_GetNodeCount(Node* Head) {
	unsigned int Count = 0;
	Node* Current = Head;
	while (Current != NULL) {
		Current = Current->NextNode;
		Count++;
	}
	return Count;
}
```

## 더블링크드 리스트 예제 프로그램
```c
void main() {
	int Count = 0; //노드의 개수
	Node* List = NULL; //노드가 없는 NULL 리스트
	Node* NewNode = NULL;
	Node* Current = NULL;

	//노드 5개 추가
	for (int i = 0; i < 5; i++) {
		NewNode = DLL_CreateNode(i);
		DLL_AppendNode(&List, NewNode);
	}

	//리스트 출력
	Count = DLL_GetNodeCount(List);
	for (int i = 0; i < Count; i++) {
		Current = DLL_GetNodeAt(List, i);
		printf("List[%d] : %d\n", i, Current->Data);
	}

	//리스트의 세번째 칸 뒤에 노드 삽입
	printf("\nInserting 3000 After [2]...\n");

	Current = DLL_GetNodeAt(List, 2);
	NewNode = DLL_CreateNode(3000);
	DLL_InsertAfter(Current, NewNode);

	//리스트 출력
	Count = DLL_GetNodeCount(List);
	for (int i = 0; i < Count; i++) {
		Current = DLL_GetNodeAt(List, i);
		printf("List[%d] : %d\n", i, Current->Data);
	}

	// 모든 노드를 메모리에서 제거
	printf("\nDestorying List..\n");
	Count = DLL_GetNodeCount(List);

	for (int i = 0; i < Count; i++) {
		Current = DLL_GetNodeAt(List, 0);
		if (Current != NULL) {
			DLL_RemoveNode(&List, Current);
			DLL_DestoryNode(Current);
		}
	}
}
```

# 환형 링크드 리스트
- Head가 Tail을 물고 있는 형태의 Linked List
- 그것말고는 다른 Linked List와 동일합니다.
- Tail의 NextNode가 Head를 가리키게 만들면 된다.
- 시작을 알면 끝을 알 수 있고 끝을 알면 시작을 알 수 있다.

## 환형 더블 링크드 리스트의 주요연산
- 링크드 리스트로도 환형 링크드 리스트를 구현할 수 있다.
- 지금은 더블 링크드 리스트로 환형 링크드 리스트를 구현해볼 것이다.
- 항상 다음의 두가지 사항을 염두해 둬야 한다.
	- Tail은 Head의 '이전 노드'이다.
 	- Head의 Tail은 '다음 노드'이다.
 
## 노드 추가연산
- 새로운 노드는 헤드가 되고, 헤드의 이전 노드는 헤드가 되며, 헤드의 다음 노드 역시 헤드가 된다.

![image](https://github.com/to7485/Clang/assets/54658614/2ad131d6-489a-4b5b-9d54-62f19dc445c3)

```c
//노드 추가
void CDLL_AppendNode(Node** Head, Node* NewNode) {
	if ((*Head) == NULL) {
		*Head = NewNode;
		(*Head)->NextNode = *Head;
		(*Head)->PrevNode = *Head;
	}
	else {
		//테일과 헤드 사이에 NewNode를 삽입한다.
		Node* Tail = (*Head)->PrevNode;

		Tail->NextNode->PrevNode = NewNode;
		Tail->NextNode = NewNode;

		NewNode->NextNode = (*Head);
		NewNode->PrevNode = Tail; //새로운 테일의 PrevNode가 기존의 Tail을 가리킨다.
	}
}
```

## 노드의 삭제
- 테일과 헤드가 연결되어 있다는 사실에 주의만 하자.
```c
//노드 제거
void CDLL_RemoveNode(Node** Head, Node* Remove) {
	if (*Head == Remove) {
		(*Head)->PrevNode->NextNode = Remove->NextNode;
		(*Head)->NextNode->PrevNode = Remove->PrevNode;

		*Head = Remove->NextNode;

		Remove->PrevNode = NULL;
		Remove->NextNode = NULL;
	}
	else {
		Remove->PrevNode->NextNode = Remove->NextNode;
		Remove->NextNode->PrevNode = Remove->PrevNode;

		Remove->PrevNode = NULL;
		Remove->NextNode = NULL;
	}
}
```
## 환형 리스트 프로그램 예제
```c
#include <stdio.h>

typedef int ElementType;

typedef struct tagNode {
	ElementType Data;
	struct tagNode* PrevNode;
	struct tagNode* NextNode;
}Node;

//노드 생성
Node* CDLL_CreateNode(ElementType NewData) {
	Node* NewNode = (Node*)malloc(sizeof(Node));

	NewNode->Data = NewData;
	NewNode->PrevNode = NULL;
	NewNode->NextNode = NULL;

	return NewNode;
}

//노드의 소멸
void CDLL_DestroyNode(Node* Node) {
	free(Node);
}

//노드 추가
void CDLL_AppendNode(Node** Head, Node* NewNode) {
	if ((*Head) == NULL) {
		*Head = NewNode;
		(*Head)->NextNode = *Head;
		(*Head)->PrevNode = *Head;
	}
	else {
		//테일과 헤드 사이에 NewNode를 삽입한다.
		Node* Tail = (*Head)->PrevNode;

		Tail->NextNode->PrevNode = NewNode;
		Tail->NextNode = NewNode;

		NewNode->NextNode = (*Head);
		NewNode->PrevNode = Tail; //새로운 테일의 PrevNode가 기존의 Tail을 가리킨다.
	}
}

//노드 삽입
void CDLL_InsertAfter(Node* Current, Node* NewNode) {
	NewNode->NextNode = Current->NextNode;
	NewNode->PrevNode = Current;

	if (Current->NextNode != NULL) {
		Current->NextNode->PrevNode = NewNode;
		Current->NextNode = NewNode;

	}
}

//노드 제거
void CDLL_RemoveNode(Node** Head, Node* Remove) {
	if (*Head == Remove) {
		(*Head)->PrevNode->NextNode = Remove->NextNode;
		(*Head)->NextNode->PrevNode = Remove->PrevNode;

		*Head = Remove->NextNode;

		Remove->PrevNode = NULL;
		Remove->NextNode = NULL;
	}
	else {
		Remove->PrevNode->NextNode = Remove->NextNode;
		Remove->NextNode->PrevNode = Remove->PrevNode;

		Remove->PrevNode = NULL;
		Remove->NextNode = NULL;
	}
}

//노드 탐색
Node* CDLL_GetNodeAt(Node* Head, int Location) {
	Node* Current = Head;

	while (Current != NULL && (--Location) >= 0) {
		Current = Current->NextNode;
	}
	return Current;
}

//노드 개수 세기
int CDLL_GetNodeCount(Node* Head) {
	unsigned int Count = 0;
	Node* Current = Head;

	while (Current != NULL) {
		Current = Current->NextNode;
		Count++;

		if (Current == Head) {
			break;
		}
	}
	return Count;
}

void PrintNode(Node* _Node) {
	if (_Node->PrevNode == NULL) {
		printf("Prev : NULL");
	}
	else {
		printf("Prev : %d", _Node->PrevNode->Data);
	}
	printf("Current: %d", _Node->Data);

	if (_Node->NextNode == NULL) {
		printf("Next: NULL\n");
	}
	else {
		printf("Next: %d\n", _Node->NextNode->Data);
	}
}

void main() {
	int Count = 0;
	Node* List = NULL;
	Node* NewNode = NULL;
	Node* Current = NULL;

	//노드 5개 추가
	for (int i = 0; i < 5; i++) {
		NewNode = CDLL_CreateNode(i);
		CDLL_AppendNode(&List, NewNode);
	}

	//리스트의 출력
	Count = CDLL_GetNodeCount(List);
	for (int i = 0; i < Count; i++) {
		Current = CDLL_GetNodeAt(List,i);
		printf("List[%d] : %d\n", i, Current->Data);
	}

	//리스트의 세번째 칸 뒤에 노드 삽입
	printf("\nInserting 3000 After [2]...\n");

	Current = CDLL_GetNodeAt(List, 2);
	NewNode = CDLL_CreateNode(3000);
	CDLL_InsertAfter(Current, NewNode);

	printf("\nRemoving Node at 2...\n");

	Current = CDLL_GetNodeAt(List,2);
	CDLL_RemoveNode(&List, Current);
	CDLL_DestroyNode(Current);

	//리스트 출력
	//(노드 개수의 2배만큼 루프를 돌며 환형임을 확인한다.
	Count = CDLL_GetNodeCount(List);
	for (int i = 0; i < Count * 2; i++) {
		if (i == 0) {
			Current = List;
		}
		else {
			Current = Current->NextNode;
		}
		printf("List[%d] : %d\n", i, Current->Data);
	}
	//모든 노드를 메모리에서 제거
	printf("\nDestroying List...\n");
	Count = CDLL_GetNodeCount(List);

	for (int i = 0; i < Count; i++) {
		Current = CDLL_GetNodeAt(List, 0);

		if (Current != NULL) {
			CDLL_RemoveNode(&List, Current);
			CDLL_DestroyNode(Current);
		}
	}
}
```
