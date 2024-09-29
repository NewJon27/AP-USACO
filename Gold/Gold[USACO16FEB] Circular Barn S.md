# [USACO16FEB] Circular Barn S

## 题目背景

(https://usaco.org/index.php?page=viewproblem2&cpid=621)

## 题目描述

作为当代建筑的爱好者，Farmer John 建造了一个圆形新谷仓，谷仓内部 n 个房间排成环形（3 <= n \<= 1000），按顺时针顺序编号为 1.....n，每个房间都有通往与其相邻的左右房间的门，还有一扇门通往外面。

现在 FJ 有 n 头奶牛，他的目标是让每个房间恰好有一头奶牛。然而不幸的是，现在奶牛们随意呆在某个房间里，第 i 个房间里有 c_i 头奶牛。保证 Sum c_i =n。

FJ 决定采用这样的方法来解决这个问题：让某些奶牛**顺时针**穿过某些房间到达指定的位置。如果一头奶牛穿过了 d扇门，他消耗的能量为 d^2。你需要帮 FJ 算出所有奶牛消耗的能量和最小值是多少。

## 输入格式

第一行一个整数 n，接下来 n 行，第 i 行一个整数 c_i。

## 输出格式

输出所有奶牛最小消耗能量和。

## 样例 #1

### 样例输入 #1

```
10
1
0
0
2
0
0
1
2
2
2
```

### 样例输出 #1

```
33
```
Answers 1 in Python
```
n = int(input())  # 读取房间数量
a = []            # 存放每头奶牛所在房间编号的列表
cnt = 0           # 当前房间编号
maxx = -float('inf')  # 存放差值数组 b 的最大值
p = 0             # 存放差值数组 b 的最大值对应的索引
ans = 0           # 最后输出的最小能量

# 构建奶牛所在房间的列表 a
for _ in range(n):
    x = int(input())  # 读取当前房间的奶牛数量
    while x:
        a.append(cnt)  # 将当前房间编号添加到列表中
        x -= 1
    cnt += 1

# 构建差值数组 b
b = [a[i] - i for i in range(n)]

# 找出差值数组 b 中的最大值及其对应的索引
for i in range(n):
    if b[i] > maxx:
        maxx = b[i]
        p = i

# 根据最大值位置 p 构建目标位置数组 c
c = [0] * n
c[p] = a[p]

# 从 p 向左构建目标位置数组
for i in range(p-1, -1, -1):
    c[i] = (c[i+1] - 1) % n

# 从 p 向右构建目标位置数组
for i in range(p+1, n):
    c[i] = (c[i-1] + 1) % n

# 计算总能量
for i in range(n):
    if c[i] < a[i]:
        c[i] += n
    ans += (c[i] - a[i]) ** 2

print(ans)

```
Answers 2 by G1-3 Andy Chen
```
def array_rfind(a):
    for i in range(len(a)-1,-1,-1):
        if a[i]==0:
            return i
def back_to_front(a):
    array1=[]
    array1.append(a[-1])
    for i in range(len(a)-1):
        array1.append(a[i])
    return array1

output=0
n=int(input())
warehouse=[]
for i in range(n):
    warehouse.append(int(input()))
count=0
while 0 in warehouse:
    k=array_rfind(warehouse)
    K=array_rfind(warehouse)
    length=0
    while True:
        if warehouse[k]!=0:
            warehouse[K]+=1
            warehouse[k]-=1
            output+=length**2
            break
        else:
            length+=1
            k-=1
            if k<0:
                k=len(warehouse)-1
    warehouse=back_to_front(warehouse)
print(output)
```

