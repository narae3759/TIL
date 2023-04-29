# [level 1] 시저 암호 - 12926 

> 출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges, 
[문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/12926) 

### 문제 설명

<p>어떤 문장의 각 알파벳을 일정한 거리만큼 밀어서 다른 알파벳으로 바꾸는 암호화 방식을 시저 암호라고 합니다.  예를 들어 "AB"는 1만큼 밀면 "BC"가 되고, 3만큼 밀면 "DE"가 됩니다. "z"는 1만큼 밀면 "a"가 됩니다. 문자열 s와 거리 n을 입력받아 s를 n만큼 민 암호문을 만드는 함수, solution을 완성해 보세요.</p>

<h5>제한 조건</h5>

<ul>
<li>공백은 아무리 밀어도 공백입니다.</li>
<li>s는 알파벳 소문자, 대문자, 공백으로만 이루어져 있습니다.</li>
<li>s의 길이는 8000이하입니다.</li>
<li>n은 1 이상, 25이하인 자연수입니다.</li>
</ul>

<h5>입출력 예</h5>
<table class="table">
        <thead><tr>
<th>s</th>
<th>n</th>
<th>result</th>
</tr>
</thead>
        <tbody><tr>
<td>"AB"</td>
<td>1</td>
<td>"BC"</td>
</tr>
<tr>
<td>"z"</td>
<td>1</td>
<td>"a"</td>
</tr>
<tr>
<td>"a B z"</td>
<td>4</td>
<td>"e F d"</td>
</tr>
</tbody>
      </table>


# **문제 풀이**
## 📌**핵심**
* 대/소문자를 변환할 수 있는가?
* 인덱스가 넘치는 경우 이를 해결할 수 있는가?
* 예외(`' '`)를 잘 처리할 수 있는가?

## 📌**해결 방법**
* **내가 생각한 풀이**
    * 알파벳의 반복이기 때문에 나머지를 인덱스로 이용 
    * 조건문을 통해 
        1. 예외를 처리하고 
        2. 인덱스를 설정한 후 
        3. 대/소문자에 따라 변환

* **새로운 풀이**
    * ***유니코드***를 이용하여 
        1. 문자를 유니코드로 변환 (a~z : 97~122)
        2. 거리만큼 덧셈 
        3. 유니코드를 문자로 변환 
        4. 대/소문자에 따라 변환하는 과정을 진행
    

## 📌**Python 코드**
### **1) 내가 생각한 풀이**
```python
def solution(s, n):
    answer = ''
    seq = 'abcdefghijklmnopqrstuvwxyz'
    alphabet = dict([(x, i) for i, x in enumerate(seq)])
    for t in s:
        if t == ' ':
            answer += ' '
        else:
            find = seq[(alphabet[t.lower()] + n) % len(seq)]
            if t.isupper():
                answer += find.upper()
            else:
                answer += find
    
    return answer
```

### **2) 새로운 풀이**
```python
def solution(s, n):
    answer = ''
    ord_max = ord('z')
    
    for t in s:
        if t == ' ':
            answer += ' '
        else:
            ord_t = ord(t.lower()) + n - 26 * (ord(t.lower()) + n > ord_max)
            answer += chr(ord_t) if t.islower() else chr(ord_t).upper()
            
    return answer
```