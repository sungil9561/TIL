# Matplotlib

> 파이썬에서 데이터를 그래프나 차트로 시각화할 수 있는 라이브러리

```python
import matplotlib.pyplot as plt
```

[Tutorial](https://wikidocs.net/book/5011)



## Matplotlib 기초

### Matplotlib 구조

![image-20220304114458549](C:\Users\sungi\TIL\Python_DataAnalysis\assets\image-20220304114458549.png)



### 그래프 그려보기

##### plot

- [matplotliob.pyplot.figure](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.figure.html#matplotlib.pyplot.figure)를 이용해 figure를 생성할 수 있음

```python
x = [1, 2, 3, 4, 5]
y = [1, 2, 3, 4, 5]
plt.plot(x, y)
plt.title('First Plot')
plt.xlabel('x')
plt.ylabel('y')
```

##### fig, ax 생성하기

```python
fig, ax = plt.subplots()
ax.plot(x, y)
ax.set_title('First Plot')
ax.set_xlabel('x')
ax.set_ylabel('y')
```



### 저장하기

```python
fig.set_dip(300)
fig.savefig('first_plot.png')
```



### 여러개 그래프 그리기

- subplot은 2차원 배열로 생성

```python
x = np.linspace(0, np.pi*4, 100)
fig, axes = plt.subplots(2, 1)
axes[0].plot(x, np.sin(x))
axes[1].plot(x, np.cos(x))
```

```python
x = np.linspace(0, np.pi*4, 100)
fig, axes = plt.subplots(2, 3)
axes[0, 0].plot(x, np.sin(x))
axes[1, 2].plot(x, np.cos(x))
```



## Line 그래프

>[matplotlib cheat sheet](https://matplotlib.org/cheatsheets/_images/cheatsheets-1.png)

### Line plot

```python
fig, ax = plt.subpolots()
x = np.arange(15)
y = x**2
ax.plot(
	x, y, 
    linestyle=":",
    marker="*"
    color="#524FA1"
)
```



### Line style

```python
ax.plot(x, x**2, linestyle="-")
```

![image-20220304130450938](C:\Users\sungi\TIL\Python_DataAnalysis\assets\image-20220304130450938.png)

- `-`, `--`, `-.`, `:`



### Color

```python
ax.plot(x, x**2, color="r")
```

- `r, g, b`, `green`, `0.8`, `#524FA1`



### Marker

```python
ax.plot(x, x**2, marker=".")
```

- `.`, `o`, `v`, `s`, `*`



### 축 경계 조정하기

```python
ax.set_xlim(-2, 12)
ax.set_ylim(-1.5, 1.5)
```



### 범례

```python
ax.legend(
	loc='upper right',
    shadow=True,
    fancybox=True,
    borderpad=2
)
```



## Scatter

![image-20220304132556909](C:\Users\sungi\TIL\Python_DataAnalysis\assets\image-20220304132556909.png)

```python
ax.plot(
	x, x**2, 'o',
    markersize=15,
    markerfacecolor='white',
    markeredgecolor='blue'
)
```

```python
x = np.random.randn(50)
y = np.random.randn(50)
colors = np.random.randint(0, 100, 50)
sizes = 500 * np.pi * np.random.rand(50) ** 2
ax.scatter(
	x, y, c=colors, s=sizes, alpha=0.3
)
```



## Bar & Histogram

### Bar plot

![image-20220304132608833](C:\Users\sungi\TIL\Python_DataAnalysis\assets\image-20220304132608833.png)

```python
ax.bar(x, x*2)
```



### Histogram

![image-20220304132750273](C:\Users\sungi\TIL\Python_DataAnalysis\assets\image-20220304132750273.png)

```python
ax.hist(data, bins=50)
```



## Matplotlib with Pandas

![image-20220304133056993](C:\Users\sungi\TIL\Python_DataAnalysis\assets\image-20220304133056993.png)

```python
df = pd.read_csv('./president_heights.csv')
fig, ax = plt.subplots()
ax.plot(df['order'], df['height(cm)'], label='height')
ax.set_xlabel('order')
ax.set_ylabel('height(cm)')
```
