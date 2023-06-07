# **목차** 
* [그래프 여러 개 한꺼번에 그리기](#그래프-여러-개-한꺼번에-그리기)
* [legend 설정하기](#legend-설정하기)
* [그래프에 text 추가하기](#그래프에-text-추가하기)

# **그래프 여러 개 한꺼번에 그리기**

## **방법 1. `plt.subplots()`**

```python
fig, ax = plt.subplots(nrow, ncol, figsize, options...)

df.plot(ax=ax[i,j])         # pandas dataframe을 통한 plot
ax[i,j].plot()              # ax를 통한 plot
```

* plot의 배치가 1행 또는 1열인 경우에는 `ax[i]`로 표현한다.
* plots 비율 조정 : `gridspec_kw={'height_ratios':[3,1]}`<br>
: top plot과 bottom plot의 height 비율을 2:1로 한다. 
* plots의 축 공유 : `sharex=True, sharey=True`

## **방법 2. `plt.subplot()`**
for loop를 돌리는데 유용하게 사용된다. 
```python
fig = plt.figure(figsize, options...)

ax = plt.subplot(nrow, nrow, i)     # nrow * ncol 크기에서 i번째 그래프임을 의미 
```


## **Tip 1. 그래프 사이 간격 조정하기**

```python
plt.subplots_adjust(hspace, wspace)
```

* `hspace` : 세로 간격을 조정한다. 
* `wspace` : 가로 간격을 조정한다. 
* 보통 0 ~ 0.5 값으로 설정하면 잘 조정되는 것 같다.

## **Tip 2. 큰 제목 설정하기**
y값 조정을 통해 아래 그래프와 겹치는 문제를 해결할 수 있다. 

```python
plt.subtitle(text, size, y=1)
```


---

# **legend 설정하기**

## **Tip 1. 범례가 너무 많아 legend를 쓰지 않고 싶다.**

```python
# Method 1
ax.plot(legend=False)
# Method 2
ax.plot(legend='_nolegend_')
# Method 3
ax.get_legend().remove()
# Method 4
ax.get_legend().set_visible(False)
# Method 5
ax.legend_ = None
```
* [참고자료. https://www.geeksforgeeks.org/how-to-remove-the-legend-in-matplotlib/](https://www.geeksforgeeks.org/how-to-remove-the-legend-in-matplotlib/)

## **Tip 2. legend 위치 설정하기**

범례가 너무 크거나 그래프를 방해할 때 아래의 옵션을 통해 그래프 밖으로 위치시킬 수 있다.

```python
ax.legend(loc, bbox_to_anchor)
```
* `loc` : 범례 위치(best, upper right, right, center, ...)
* `bbox_to_anchor` : 기준점 위치


* [참고자료. https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.legend.html](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.legend.html)

---

# **그래프에 text 추가하기**

```
ax.text(x, y, value, horizontalalignment, verticalalignment)
```

* `horizontalalignment`, `verticalalignment`는 text를 위치시킬 기준점이다.
    * `horizontalalignment` : center, right, left
    * `verticalalignment` : center, top, bottom, baseline