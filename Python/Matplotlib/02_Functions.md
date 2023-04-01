# **Functions**

```python
import matplotlib.pyplot as plt
from matplotlib import dates
```

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
            yaxis.set_major_locator()<br>
            xaxis.set_minor_locator()<br>
            yaxis.set_minor_locator()
        </td>
        <td>
            x, y축의 major(minor) tick을 설정할 규칙을 정한다.<br>
            datetime인 경우 dates.DateLocator()이용(
                <a href=(https://matplotlib.org/stable/api/dates_api.html)>바로가기</a>)
        </td>
    </tr>
    <tr>
        <td style="text-align:center;">
            xaxis.set_major_formatter()<br>
            yaxis.set_major_formatter()<br>
            xaxis.set_minor_formatter()<br>
            yaxis.set_minor_formatter()
        </td>
        <td>
            x, y축의 major(minor) tick의 format을 설정한다.<br>
            datetime인 경우 dates.DateFormatter()이용(
                <a href=(https://matplotlib.org/stable/api/dates_api.html)>바로가기</a>)</td>
    </tr>
</table>