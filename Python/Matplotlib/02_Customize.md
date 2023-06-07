# **목차** 
* [ax.set(), 축 정보 설정하기](#축-정보-설정하기)
* [ax.aixs('off'), 축 정보 모두 지우기](#축-정보-모두-지우기)
* [y축 scientific format으로 변경하기](#scientific-format)

# **축 정보 한번에 설정하기**

```python
ax.set(xlabel, ylabel, xticklabels, yticklabels, xlim, ylim, title, ...)
```
* `ax.set()`을 이용하면 축에 관한 모든 정보를 한번에 지정할 수 있다. 
* 따로 조정하고 싶을 때에는 `ax.set_`뒤에 조정하고자 하는 option을 붙이면 된다. 

## **Tip. 그래프 타이틀 설정**
* 가장 많이 수정하는 옵션 : bold, fontsize, 그래프와의 간격

    ```python
    ax.set_title(title, pad, fontweight, size)
    ```

# **축 정보 모두 지우기**
모든 축을 그리고 싶지 않을 때 사용한다. 이미지를 ax를 이용하여 출력하고 싶을 때 주로 사용한다. 

```python
ax.axis('off')
```

# **Scientific Format**
그래프를 여러 개 그릴 때 y축의 표현을 통일하고 싶을 때 주로 사용한다. 

```python
plt.ticklabel_format(axis='both/x/y', style='sci',scilimit=(n,m))
```
