<!-- > **Reference**<br>
> *  -->

# **1. 한글 폰트 적용 방법**
## **1) Local**
1. 한글 폰트 설치(ex. [Google Fonts](https://fonts.google.com/))
2. 한글 폰트 등록,다음의 디렉토리를 들어가서 fonts 폴더를 찾고 그 안에 한글 ttf파일을 넣는다.
    ```python
    mpl.matplotlib_fname()
    ```
3. 재시작, 다음 폴더 안의 파일들은 모두 삭제한 후, 파이선을 재시작한다. 
    ```python
    mpl.get_cachedir()
    ```
4. 한글 폰트 설정
    ```python
    mpl.rcParams['font.family'] = 'NanumGothic'
    mpl.rcParams['axes.unicode_minus'] = False
    ```

## **2) Colab**
```python
# 폰트 설치
!apt -qq -y install fonts-nanum 
!sudo fc-cache -fv
!rm ~/.cache/matplotlib -rf
```
```python
import matplotlib as mpl
import matplotlib.pyplot as plt

plt.rc('font', family='NanumGothic')            # matplotllib
mpl.rcParams['axes.unicode_minus'] = False      # minus 처리
```

# **2. `Matplotlib.pyplot`**

```python 
import matplotlib.pyplot as plt
```



# **3. Functions**

<table style="width:90%">
    <tr>
        <th style="width:20%; font-weight:bold; text-align:center">code</th>
        <th style="width:80%; font-weight:bold; text-align:center">설명</th>      
    </tr>
    <tr>
        <td style="text-align:center;">
            set_xlim()<br>
            set_ylim()
        </td>
        <td>x, y축의 범위를 설정할 수 있다.<br>
            set(xlim='', ylim='')으로 설정할 수도 있다.</td>
    </tr>
    <tr>
        <td style="text-align:center;">
            set_xlabel()<br>
            set_ylabel()
        </td>
        <td>x, y축의 라벨을 설정할 수 있다.<br>
            set(xlabel='', ylabel='')으로 설정할 수도 있다.</td>
    </tr>
    <tr>
        <td style="text-align:center;">
            set_xticks([pos],[label])<br>
            set_yticks([pos],[label])
        </td>
        <td>x, y축의 xtick의 위치와 label을 설정할 수 있다.</td>
    </tr>
    <tr>
        <td style="text-align:center;">
            set_xticklabels()<br>
            set_yticklabels()
        </td>
        <td>xtick이 고정되어 있을 때, x, y축의 tick 라벨을 설정할 수 있다.</td>
    </tr>
    <tr>
        <td style="text-align:center;">
            xaxis.set_major_locator()<br>
            yaxis.set_major_locator()
        </td>
        <td>x, y축의 major tick을 설정할 규칙을 정한다.</td>
    </tr>
    <tr>
        <td style="text-align:center;">
            xaxis.set_minor_locator()<br>
            yaxis.set_minor_locator()
        </td>
        <td>x, y축의 minor tick을 설정할 규칙을 정한다.</td>
    </tr>
    <tr>
        <td style="text-align:center;">
            xaxis.set_major_formatter()<br>
            yaxis.set_major_formatter()
        </td>
        <td>x, y축의 major tick의 format을 설정한다.</td>
    </tr>
    <tr>
        <td style="text-align:center;">
            xaxis.set_minor_formatter()<br>
            yaxis.set_minor_formatter()
        </td>
        <td>x, y축의 minor tick의 format을 설정한다.</td>
    </tr>
</table>