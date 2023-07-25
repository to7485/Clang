# 스택
- Stack은 건초나 짚더미처럼 뭔가를 쌓아올린 더미를 뜻합니다.
- Stack ADT도 데이터를 바닥부터 쌓아올리는 구조로 되어있다.
- 스택에서는 <b>가장 마지막에 들어간 데이터가 제일 먼저 나오고(Last In First Out), 가장 먼저 들어간 데이터는 가장 나중에 나온다(First In Last Out)</b>
- C언어의 Stack 메모리 영역도 자료구조 Stack으로 구현이 되어 있습니다. 그래서 지역변수는 스택에 할당된다 라고 표현합니다.
- 스택은 소프트웨어 분야에서 매우 중요한 역할을 맡고 있다.
- 자동 메모리가 스택을 기반으로 동작하고 거의 대부분의 네트워크 프로토콜도 스택을 기반으로 구성되어 있습니다.
- 뿐만 아니라 컴파일러의 구문 분석기, 이미지 편집 프로그램의 되돌리기(Undo)기능도 스택을 이용하고 있다.

## 스택의 핵심기능 : 삽입과 제거 연산
- 스택 ADT의 주요 기능은 삽입(Push)과 제거(Pop)연산 이다.
- 그 외의 기능들은 두 연산을 위한 보조 연산에 지나지 않는다.

- 삽입 연산은 스택 위에 새로운 노드(요소)를 '쌓는'일을 합니다.

![image](https://github.com/to7485/Clang/assets/54658614/5bfd3cf0-46d3-4683-96ed-619ca3278e38)

- 반대로 제거 연산은 스택에서 최상위 노드를'걷어'낸다.

![image](https://github.com/to7485/Clang/assets/54658614/b3f51f54-9acb-4059-84b4-3a3f6099882f)

## 배열로 구현하는 스택
- 배열을 이용한 스택은 용량을 동적으로 변경하는 비용이 크다는 단점이 있지만 구현이 간단하다는 장점 있다.
- 배열 기반의 스택은 각 노드를 동적으로 생성하고 제거하는 대신, 스택 생성 초기에 사용자가 부여한 용량만큼 노드를 한꺼번에 생성한다.
- 최상위 노드의 위치를 나타내는 변수를 두고 삽입과 제거 연산을 수행한다.

## 노드의 표현
- 노드가 존재하는 위치는 배열의 인덱스로 알 수 있기 때문에 노드에 대한 포인터가 필요 없다.
```c
typedef int ElementType;

typedef struct tagNode{
ElementType Data;
} Node;
```

## 스택의 표현
- 배열 기반의 스택은 다음 세가지 필드를 갖고 있어야 한다.
  - 용량
  - 최상위 노드의 위치
  - 노드 배열
 
- 용량은 스택이 얼마만큼의 노드를 가질 수 있는지 알기 위해 사용된다.
- 최상위 노드의 위치는 삽입/제거 연산을 할 때 최상위 노드에 접근할 수 있게 도와준다.
- 노드 배열은 스택에 쌓이는 노드를 보관하는데 사용된다.

```c
typedef struct tagArrayStack{
  int Capacity; //노드의 개수
  int Top; //최상위 노드의 위치
  Node* Nodes; //노드 배열
} ArrayStack;
```

- 노드배열을 자유 저장소(Heap)에 할당하고 Node포인터는 자유 저장소(Heap)에 할당된 배열을 가리키는 용도로 사용할 것이다.

![image](https://github.com/to7485/Clang/assets/54658614/96cef174-d4ab-45d4-9a35-7bc2b77a9ef0)

## 스택 및 노드 생성/소멸

### 스택의 생성
- 첫번째 인자는 ArrayStack 구조체이고, 두번재는 스택의 용량을 나타내는 노드의 개수이다.
- 처음 호출된 malloc()은 ArrayStack을 자유저장소(Heap)에 쌓기 위해 사용됐고
- 두번재 호출된 malloc()은 매개변수로 입력된 개수만큼 노드를 미리 생성하는데 사용이 되었다.
- ArrayStack의 Capacity는 배열의 용량을 저장하고 최상위 노드의 위치를 가리키는 Top을 -1로 초기화 한다.
- Top을 0이 아닌 -1로 초기화를 하는 이유는 C언어에서 첫 번째 배열의 요소를 가리키는 첨자가 0이므로 비어있는 스택의 최상위 위치가 이보다 작아야 하기 때문이다.
- Top은 노드가 삽입될 때마다 1씩 증가하고 노드가 삭제될 때마다 1씩 감소합니다.
```c
void AS_CreateStack(ArrayStack** Stack, int Capacity) {
	//스택을 자유 저장소(Heap)에 생성
	(*Stack) = (ArrayStack*)malloc(sizeof(ArrayStack));

	//입력된 Capacity만큼의 노드를 자유 저장소(Heap)에 생성
	(*Stack)->Nodes = (Node*)malloc(sizeof(Node)*Capacity);

	//Capacity 및 Top의 초기화
	(*Stack)->Capacity = Capacity;
	(*Stack)->Top = -1;
}
```

### 스택의 삭제
```c
void AS_DestroyStack(ArrayStack* Stack) {
	//노드를 자유 저장소에서 해제
	free(Stack->Nodes);

	//스택을 자유 저장소에서 해제
	free(Stack);
}
```






