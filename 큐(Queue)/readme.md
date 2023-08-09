# 큐
- 먼저 들어간 데이터가 먼저 나오는 (FIFO,선입선출)자료구조를 큐(Queue)라고 한다.
- 입력과 출력 창구가 따로 존재하고, 제일 먼저 들어간 데이터가 제일 먼저 나온다.
- 큐는 작업을 처리하는 요소에 부하를 주지 않으면서도 처리 능력을 넘어서는 작업들도 놓치지 않고 수용할 수 있게 도와줍니다.
- 30인승 롤러코스터에 200명의 손님이 몰렸다. 먼저온 손님 30명만 태우고 170명은 큐에서 기다리게 해야한다.
- 손님이 몰린다고 해서 30명이 정원인 롤러코스터에 50명을 태우면 안된다.

## 큐의 핵심 기능
- 큐의 가장 앞 요소를 전단, 가장 마지막 요소를 후단이라고 부릅니다.

![image](https://github.com/to7485/Clang/assets/54658614/f22a6f9b-c336-481b-a104-eb4e92b1614b)

- 큐의 경우 삽입연산은 후단, 제거 연산은 전단에서 각각 수행이 된다.
- 삽입은 후단에 노드를 덧붙여서 새로운 후단을 만드는 연산이다.

![image](https://github.com/to7485/Clang/assets/54658614/b11711a4-cac0-4b5e-97a3-f05f0914908a)

제거는 전단의 노드를 없애서 전단 뒤에 있는 노드를 새로운 전단으로 만드는 연산을 말한다.

![image](https://github.com/to7485/Clang/assets/54658614/4ce87a71-a0ae-4ffc-a691-358b84b4798b)

## 순환 큐
- 시작과 끝을 연결해서 효율적인 삽입/삭제 연산이 가능하도록 고안된 큐
- C언어의 경우 배열의 시작과 끝을 연결하는 방법을 제공하지 않기 때문에 이 구조를 직접 코드로 구현해야 한다.

## 공백과 포화상태
- 큐가 포화 상태일 때뿐 아니라 공백 상태일 때도 전단과 후단이 만나기 때문에 두 상태를 구분하는 방법을 찾아야 한다.

![image](https://github.com/to7485/Clang/assets/54658614/54738f5d-3d93-4e6e-86aa-8781eaa106a5)

- 큐 배열을 생성할 때 실제 용량보다 1만큼 더 크게 만들어서 전단과 후단(실제 후단)사이를 비우는것이다.
- 이렇게 하면 큐가 공백 상태일 때 전단과 후단이 같은 곳을 가리키고, 큐가 포화 상태일 때 후단이 전단보다 1 작은 값을 가지므로 상태 구분이 용이하다.

![image](https://github.com/to7485/Clang/assets/54658614/4478e18d-8edc-40c0-9a3f-d59d7d28940b)

## 순환큐의 기본연산
- 순환 큐는 배열을 기반으로 구현되며 삽입과 삭제 연산이 이루어질 때 전단과 후단을 변경함으로써 큐가 공백상태인지 포화상태인지 확인한다.

## 순환 큐 선언
- 순환 큐의 노드 구조체 선언
```c
typedef int ElementType;

typedef struct Node {
	ElementType Data;
};
```
## 순환큐 구조체
- 순환큐를 나타내는 구조체는 용량(Capacity),전단의 위치(Front), 후단의 위치(Rear), 순환 큐 요소의 배열에 대한 포인터를 갖고 있다.
```c
typedef struct CircularQueue {
	int Capacity;
	int Front;
	int Rear;

	Node* Nodes;
}CircularQueue;
```
- 구조체의 Nodes 포인터가 가리키는 배열은 Heap영역에 생성된다.
- Capacity는 순환 큐의 용량, 즉 Nodex 배열의 크기를 나타내는데 Nodes를 메모리에 할당할 때는 'Capacity+1'만큼의 크기를 할당한다.
- 노드 하나를 공백/포화 상태 구분용 더미 노드로 사용하기 때문이다.
- Front는 전단의 위치를, Rear는 후단 위치를 가리킨다. 이들이 갖는 값은 실제 메모리 주소가 아니라 배열 내의 index값이다.
- Rear는 실제 후단보다 1 더 큰 값을 갖는다.

![image](https://github.com/to7485/Clang/assets/54658614/9069cb10-c021-4ba2-93f5-5d309631a0c5)

## 순환 큐 생성/소멸 연산
- 순환 큐 생성
```c
void  CQ_CreateQueue(CircularQueue** Queue, int Capacity)
{
	//  큐를 자유 저장소에 생성 
	(*Queue) = (CircularQueue*)malloc(sizeof(CircularQueue));

	//  입력된 Capacity+1 만큼의 노드를 자유 저장소에 생성 
	(*Queue)->Nodes = (Node*)malloc(sizeof(Node)* (Capacity + 1));

	(*Queue)->Capacity = Capacity;
	(*Queue)->Front = 0;
	(*Queue)->Rear = 0;
}
```
- 순환 큐 삭제
```c
void CQ_DestroyQueue(CircularQueue* Queue)
{
	free(Queue->Nodes);
	free(Queue);
}
```

## 노드 삽입 연산
- 순환 큐에서 삽입 연산 구연은 후단의 위치를 가리키는 Rear를 다루는것이 핵심이다.

```c
void CQ_Enqueue(CircularQueue* Queue, ElementType Data)
{
	int Position = 0;

  //Rear의 값이 *Queue->Capacity+1과 같다면 후단이 배열 끝에 도달했다는 의미이므로
  //Rear와 Position을 0으로 지정한다.

	if (Queue->Rear == Queue->Capacity)
	{
		Position = Queue->Rear;
		Queue->Rear = 0;
	}
	//후단이 배열 끝에 도달하지 않은 경우 else로 넘어가서
	//현재 Rear의 위치를 Position에 저장하고 Rear값을 1 증가시킨다.
	else
		Position = Queue->Rear++;

	//if~else를 거치고 나면 Nodes 배열에서 Position이 가리키는 곳에 데이터를 저장한다.
	Queue->Nodes[Position].Data = Data;
}
```

![image](https://github.com/to7485/Clang/assets/54658614/7c7f2de7-c84b-426a-985f-0e48b8db6820)

## 노드 제거 연산
- 노드 제거연산에서는 전단을 나타내는 Front를 잘 관리해야 한다.
```c
ElementType CQ_Dequeue(CircularQueue* Queue)
{
	//전단의 위치를 Position에 저장한다.
//Position은 함수가 큐의 전단에 저장되어 있던 데이터를 반환할 때 Nodes 배열의 인덱스로 사용되는 변수
	int Position = Queue->Front;


	//Front의 값이 Capacity와 같을 때(전단이 배열 끝에 도달한 경우)
//Front를 0으로 초기화 하고, 그렇지 않은 경우 Front의 값을 1만큼 증가시킨다.
	if (Queue->Front == Queue->Capacity)
		Queue->Front = 0;
	else
		Queue->Front++;

	return Queue->Nodes[Position].Data;
}
```

![image](https://github.com/to7485/Clang/assets/54658614/7ad366ff-ba05-497f-9685-1ffd9af977f7)

## 공백 상태 확인
- 전단과 후단의 값이 같으면 공백 상태라는 의미
```c
int CQ_IsEmpty(CircularQueue* Queue)
{
	return (Queue->Front == Queue->Rear);
}
```

## 포화 상태 확인
- 순환 큐가 포화 상태인지 확인할 때는 두 가지 경우를 고려해야 한다.
- 전단이 후단 앞에 있을 때 후단과 전단의 차이(Rear - Front)가 큐의 용량(Capacity)과 동일하면 순환큐는 포화상태
- 또 다른 경우는 전단이 후단과 같은 위치 또는 뒤에 있고 후단에 1을 더한 값(Rear + 1)이 전단(Front)과 동일할 때

```c
int CQ_IsFull(CircularQueue* Queue)
{
	if (Queue->Front < Queue->Rear)
		return (Queue->Rear - Queue->Front) == Queue->Capacity;
	else
		return (Queue->Rear + 1) == Queue->Front;
}
```

## 순환큐 프로그램 예제
```c
int CQ_GetSize(CircularQueue* Queue)
{
	if (Queue->Front <= Queue->Rear)
		return Queue->Rear - Queue->Front;
	else
		return Queue->Rear + (Queue->Capacity - Queue->Front) + 1;
}

void main() {
	int i;
	CircularQueue* Queue;

	CQ_CreateQueue(&Queue, 10);

	CQ_Enqueue(Queue, 1);
	CQ_Enqueue(Queue, 2);
	CQ_Enqueue(Queue, 3);
	CQ_Enqueue(Queue, 4);

	for (i = 0; i < 3; i++) {
		printf("Dequeue: %d,", CQ_Dequeue(Queue));
		printf("Front:%d, Rear: %d\n", Queue->Front, Queue->Rear);
	}

	i = 100;
	while (CQ_IsFull(Queue) == 0) {
		CQ_Enqueue(Queue, i++);
	}

	printf("Capacity: %d, Size:%d\n", Queue->Capacity, CQ_GetSize(Queue));

	while (CQ_IsEmpty(Queue) == 0) {
		printf("Dequeue: %d,", CQ_Dequeue(Queue));
		printf("Front:%d, Rear: %d\n", Queue->Front, Queue->Rear);
	}

	CQ_DestroyQueue(Queue);
}
```

## 링크드 큐

### 노드 선언
```py
typedef struct tagNode {
	char* Data;
	struct tagNode* NextNode;
}Node;
```
### 링크드 큐 구조체
```py
typedef struct tagLinkedQueue {
	Node* Front;
	Node* Rear;
	int Count;
}LinkedQueue;
```

### 노드의 생성
```py
Node* LQ_CreateNode(char* NewData) {

	Node* NewNode = (Node*)malloc(sizeof(Node));

	NewNode->Data = (char*)malloc(strlen(NewData) + 1);

	strcpy(NewNode->Data, NewData);

	NewNode->NextNode = NULL; //다음 노드에 대한 포인터는 NULL로 초기화 한다.
	return NewNode; //노드의 주소를 반환
}
```

### 노드의 소멸
```py
void LQ_DestroyNode(Node* _Node) {
	free(_Node->Data);
	free(_Node);
}
```

### 큐 생성
```py
void LQ_CreateQueue(LinkedQueue** Queue) {
	//큐를 메모리에 할당
	(*Queue) = (LinkedQueue*)malloc(sizeof(LinkedQueue));
	(*Queue)->Front = NULL;
	(*Queue)->Rear = NULL;
	(*Queue)->Count = 0;
}
```

### 큐 삭제
```py
void LQ_DestroyQueue(LinkedQueue* Queue) {
	while (!LQ_IsEmpty(Queue)) {
		Node* Popped = LQ_Dequeue(Queue);
		LQ_DestroyNode(Popped);
	}

	free(Queue);
}
```

### 노드 삽입
```py
void LQ_Enqueue(LinkedQueue* Queue, Node* NewNode) {
	if (Queue->Front == NULL) {
		Queue->Front = NewNode;
		Queue->Rear = NewNode;
		Queue->Count++;
	}
	else {
		Queue->Rear->NextNode = NewNode;
		Queue->Rear = NewNode;
		Queue->Count++;
	}
}
```
### 노드 삭제
```py
//삭제하기
Node* LQ_Dequeue(LinkedQueue* Queue) {
	//LQ_Dequeue()가 반환할 최상위 노드
	Node* Front = Queue->Front;

	//삭제하려고 봤더니 노드가 하나밖에 없었음
	if (Queue->Front->NextNode == NULL) {
		Queue->Front = NULL;
		Queue->Rear = NULL;
	}
	else {
		Queue->Front = Queue->Front->NextNode;
	}
}
```

