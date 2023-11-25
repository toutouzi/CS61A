# Python



### Efficiency

---

#### memorization 

- 统计调用fib函数的次数

``` python
def fib(n):
    if n == 0 or n == 1:
        return n
    else:
        return fib(n-2) + fib(n-1)
def count(f):
    def counted(n):
        counted.call_count += 1
        return f(n)
    counted.call_count = 0
    return counted		
```

- 优化——remember the result , 减少调用次数 f 要是pure funtion，否者会有不一样的行为 

​	`f` 要是pure funtion，否者会有不一样的行为 

``` python
def memo(f):
    cache = {}
    def memoized(n):
        if n not in cache:
            cache[n] = f(n)
        return cache[n]
    return memoized

fib = count(fib)
count_fib = fib
fib = memo(fib)    #fib = memorized
fib = count(fib)		# fib = counted
fib(30)
fib.call_count
#59
count_fib.call_count
#31
```

- **59 vs 31 :** 

<img src="./src/memoization/3.png" style="zoom:30%;" />

#### exponentiation

讨论计算方法对效率的影响

​						<img src="./src/memoization/2.png" style="zoom:30%;" />

#### space

active environment : 当前栈 ； 依赖的 parent frame 

``` python
def count_frames(f):
    def counted(n):
        counted.open_count += 1
        counted.max_count = max(counted.max_count, counted.open_count)
        result = f(n)
        counted.open_count -= 1
        return result
    counted.open_count = 0
    counted.max_count = 0
    return counted
# fib = count_frames(fib)
# fib(20)  >>> 6765
# fib.open_count  >>> 0
# fib.max_count   >>> 20
```

<img src="./src/memoization/1.png" style="zoom:30%;" />

