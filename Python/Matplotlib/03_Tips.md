
```python
import matplotlib.pyplot as plt 
```

# **1. `plt.subplots()`**

```python
fig, ax = plt.subplots(nrow, ncol, figsize, options...)

# pandas dataframe을 통한 plot
df.plot(ax=ax[i,j])

# ax를 통한 plot
ax[i,j].plot()
```

* plot의 배치가 1행 또는 1열인 경우에는 `ax[i]`로 표현한다.
* plots 비율 조정 : `gridspec_kw={'height_ratios':[3,1]}`<br>
: top plot과 bottom plot의 height 비율을 2:1로 한다. 
* plots의 축 공유 : `sharex=True, sharey=True`


