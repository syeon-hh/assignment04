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

