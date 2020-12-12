### stack与queue的区别
#### Stack ```堆栈```
* 栈顶加入，栈顶取出
* 只能对栈顶作用//即列表末尾
* 代码实现
```
class Stack:
    def __init__(self):
        self.__items = []
    def pop(self): #删除栈顶元素
        if len(self.__items) > 0 :
            a= self.__items.pop()
            return a
        else:
            raise IndexError ("ERROR: The stack is empty!")
    def peek(self): #输出栈顶元素
        if len(self.__items) > 0 :
            return self.__items[len(self.__items)-1]
        else:
            raise IndexError("ERROR: The stack is empty!")
    def push(self,item): #添加元素到栈顶
        self.__items.append(item)
    def push_list(self,a_list): #添加列表元素到栈顶
        self.__items = self.__items + a_list
    def __str__(self):
        return "Stack: {}".format(self.__items)
    def __len__(self):
        return len(self.__items)
    def clear(self):
        self.__items = []
    def multi_pop(self, number): #删除栈顶多个元素
        if number > len(self.__items):
            return "False"
        else:
            for i in range(0,number):
                self.__items.pop()
            return "True"
    def copy(self):
        a=Stack()
        for i in self.__items:
            a.push(i)
        return a
    def __eq__(self,other): #两个栈是否相同
        if not isinstance(other,Stack):
            return "False"
        else:
            if len(other) != len(self):
                return "False"
            else:
                a = other.copy()
                b = self.copy()  #self调用的就是栈本身
                for i in range(len(a)):
                    if a.pop() != b.pop():
                        return "False"
                return "True"
```
#### Queue ```队列```
* 有多种，这里是先入先出的队列
* 加入到列表尾，删除从列表首删除（可以自己规定）
* 代码实现
```
class Queue:
    def __init__(self):
        self.__items = []
    def enqueue(self,item): #添加
        self.__items.append(item)
    def dequeue(self): #删除
        if len(self.__items) == 0:
            raise IndexError("ERROR: The queue is empty!")
        else:
            return self.__items.pop(0)
    def peek(self):
        if len(self.__items) == 0:
            raise IndexError("ERROR: The queue is empty!")
        else:
            return self.__items[0]
    def __str__(self):
        return "Queue: {}".format(self.__items)
    def __len__(self):
        return len(self.__items)
    def clear(self):
        self.__items = []
    def enqueue_list(self, a_list):
        self.__items = self.__items + a_list
    def multi_dequeue(self, number):
        if len(self) < number :
            return False
        else:
            for i in range(number):
                self.dequeue()
                print(self)
            return True
```
#### CircularQueue ```循环队列```
* 从逻辑上是个圆
* 队列判空的条件是front=back，而队列判满的条件是front=（back+1)%MaxSize #但做题时前者并不为空
* 根据front和back来判断队列
* 代码实现
```
class CircularQueue:
    def __init__(self,number=8):
        self.__items = [None]* number
        self.__front = 0
        self.__back = number -1
        self.__count = 0
        self.__number = number
    def is_empty(self):
        if self.__count == 0 :
            return True
        else:
            return False
    def __str__(self):
        return "{}, front:{}, back:{}, count:{}".format(self.__items,self.__front,self.__back,self.__count)
    def is_full(self):
        return self.__count == self.__number
    def enqueue(self,item):
        if self.is_full():
            raise IndexError("ERROR: The queue is full.")
        else:
            self.__back = (self.__back +1 )% self.__number
            self.__items[self.__back] = item
            self.__count += 1
    def dequeue(self):
        if len(self.__items) == 0:
            raise IndexError("ERROR: The queue is empty!")
        else:
            self.__front = (self.__front + 1) % self.__number
            self.__count -=1
            item = self.__items[self.__front-1]
            return item
    def print_all(self):
        if self.__front == self.__back:
            return print(self.__items[self.__front])
        num = self.__back - self.__front
        for i in range(num):
            print(self.__items[self.__front + i],end = ' ')
        print(self.__items[self.__front + num])
```
