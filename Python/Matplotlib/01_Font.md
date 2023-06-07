<!-- > **Reference**<br>
> *  -->

# **한글 폰트 적용 방법**
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

## **3) Library 설치**
* 한글 폰트를 다운받지 않아도 적용시켜주는 라이브러리이다. 
* 반드시 `import matplotlib.pyplot as plt` 뒤에 실행되어야 한다.

```python
!pip install koreanize-matplotlib
```

```python
import koreanize_matplotlib
```