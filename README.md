# assignment04

## 1. leetCode225.ipynb (https://github.com/syeon-hh/assignment04/blob/main/leetCode225.ipynb)
from collections import deque

class MyStack:

    def __init__(self):
        self.q1 = deque()
        self.q2 = deque()

    def push(self, x: int) -> None:
        self.q2.append(x)  # 새 원소를 q2에 넣고
        while self.q1:
            self.q2.append(self.q1.popleft())  # q1의 모든 원소를 q2 뒤로 옮김
        self.q1, self.q2 = self.q2, self.q1  # q1이 메인 큐가 되도록 swap

    def pop(self) -> int:
        return self.q1.popleft()

    def top(self) -> int:
        return self.q1[0]

    def empty(self) -> bool:
        return not self.q1


## 2. leetCode232.ipynb (https://github.com/syeon-hh/assignment04/blob/main/leetCode232.ipynb)

class MyQueue:

    def __init__(self):
        self.in_stack = []
        self.out_stack = []

    def push(self, x: int) -> None:
        self.in_stack.append(x)

    def pop(self) -> int:
        self.move()
        return self.out_stack.pop()

    def peek(self) -> int:
        self.move()
        return self.out_stack[-1]

    def empty(self) -> bool:
        return not self.in_stack and not self.out_stack

    def move(self):
        if not self.out_stack:
            while self.in_stack:
                self.out_stack.append(self.in_stack.pop())
                
## 3. 큐 연습문제
### 1번

class ListQueue:
    def __init__(self):
        self.__queue = []

    def enqueue(self, x):
        self.__queue.insert(0, x)  # 맨 앞에 삽입

    def dequeue(self):
        return self.__queue.pop()  # 맨 뒤에서 제거 (front)

    def front(self):
        return self.__queue[-1]

    def isEmpty(self) -> bool:
        return len(self.__queue) == 0

    def dequeueAll(self):
        self.__queue.clear()

### 2번

from collections import deque

def isPalindromeStructure(s):
    q = deque()
    i = 0

    while s[i] != '$':
        q.append(s[i])
        i += 1
    i += 1  # '$' 건너뜀

    while i < len(s):
        if not q or q.pop() != s[i]:
            return False
        i += 1

    return len(q) == 0  # 남은 게 없어야 완전한 매칭

### 3번
def copyQueue(a, b):
    temp = []
    while not a.isEmpty():
        item = a.dequeue()
        b.enqueue(item)
        temp.append(item)

    for item in temp:
        a.enqueue(item)  # a도 원래대로 복원

### 4번
from collections import deque

class StackUsingQueues:
    def __init__(self):
        self.q1 = deque()
        self.q2 = deque()

    def push(self, x):
        self.q1.append(x)

    def pop(self):
        while len(self.q1) > 1:
            self.q2.append(self.q1.popleft())
        val = self.q1.popleft()

        self.q1, self.q2 = self.q2, self.q1
        return val

### 5번
class QueueUsingStacks:
    def __init__(self):
        self.s1 = []
        self.s2 = []

    def enqueue(self, x):
        self.s1.append(x)

    def dequeue(self):
        if not self.s2:
            while self.s1:
                self.s2.append(self.s1.pop())
        return self.s2.pop()

### 6번
enqueue(x)의 수행시간 = O(1) 
dequeue(x)의 수행시간 = O(n) 

### 7번
enqueue(x)의 수행시간 = O(1)
dequeue(x)의 수행시간 = O(1)


### 8번
class Deque:
    def __init__(self):
        self.__queue = []

    def addFront(self, x):
        self.__queue.append(x)

    def addRear(self, x):
        self.__queue.insert(0, x)

    def deleteFront(self):
        return self.__queue.pop() if not self.isEmpty() else None

    def deleteRear(self):
        return self.__queue.pop(0) if not self.isEmpty() else None

    def isEmpty(self):
        return len(self.__queue) == 0

    def clear(self):
        self.__queue.clear()

    def printDeque(self):
        print("Deque from front:", end=' ')
        for x in self.__queue[::-1]:
            print(x, end=' ')
        print()
