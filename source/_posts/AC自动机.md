---
title: AC自动机
date: 2023-07-17 14:09:21
categories:
- 算法
- 匹配

tags:
- 算法

---
# AC自动机

```python
def insert(str_input):  
    global cnt  
    root = 0  
    for ch in str_input:  
        index = ord(ch) - ord('a')  
        if tree[root][index] == 0:  
            cnt = cnt + 1  
            tree[root][index] = cnt  
        # sum_[tree[root][index]] += 1 前缀计数  
        root = tree[root][index]  
    end[root] += 1  # 标记结束
```

```python
def get_fail():  
    fail[0] = 0  
    que = queue.Queue()  
    for i in range(27):  
        if tree[0][i]:  
            que.put(tree[0][i])  
    while not que.empty():  
        v = que.get()  
        for i in range(27):  
            if tree[v][i]:  
                fail[tree[v][i]] = tree[fail[v]][i]  
                que.put(tree[v][i])  
            else:  
                tree[v][i] = tree[fail[v]][i]
```

```python
def query(str_input):  
    root = 0  
    ans = 0  
    for ch in list(str_input):  
        index = ord(ch) - ord('a')  
        u = root = tree[root][index]  
        while u and end[u] != -1:  
            ans += end[u]  
            end[u] = -1  
            u = fail[u]  
    return ans
```


```python
insert('ash')  
insert('shx')  
insert('bcd')  
insert('sha')  
insert('h')  
get_fail()  
print(query('ashe'))
```

	>> 2
