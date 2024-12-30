---
layout: post
title:  LeetCode - 로마자를 정수로 변환 !
image :
  path : /assets/img/problem-solving/블로그포스터-PS.png
description: 로마자를 숫자로 변환 하는 문제
sitemap: false
---

[문제 링크](https://leetcode.com/problems/roman-to-integer/description/)

---

### 문제 설명
|Symbol|Value|
|------|---|
|I|1|
|V|5|
|X|10|
|L|50|
|C|100|
|D|500|
|M|1000|

로마자와 숫자의 관계는 위 테이블과 같다.<br>
예시로 <span style="background-color:#F5F5F5"> 2 </span>는 <span style="background-color:#F5F5F5"> II </span>, <span style="background-color:#F5F5F5"> 27 </span>은 <span style="background-color:#F5F5F5"> XXVII </span>이다.

즉, input a가 <span style="background-color:#F5F5F5"> II </span>으로 주어졌을 경우에 반환 값이 int 2로 반환이 되도록 구현하는 문제이다.

---

### 문제 조건
Value가 **5이상**의 Symbol에서 <span style="background-color:#fff5b1">**감산표기법**</span>을 적용한다.

감산 표기법이란, 작은 숫자가 큰 숫자 앞에 위치할 경우, 작은 숫자를 큰 숫자에서 빼는 방식으로 숫자를 표현하는 방법입니다.

예시로, 숫자 4를 로마자로 표기하면 <span style="background-color:#F5F5F5">IV</span>가 된다.<br>
이는 5에서 1을 뺀다는 의미로 해석된다.

---

### 문제 해결
나는 해당 문제를 for문을 사용하여 로마자를 추출하고, 해당 문자와 상응하는 Value를 total이라는 변수에 더하는 방법을 생각했다. 

**Java Code**
```Java
class Solution {
    public int romanToInt(String s) {
        int total = 0;
        char storage = ' ';

        for (int i = 0; i < s.length(); i++) {
            char getChar = s.charAt(i);
            if (getChar == 'I') {
                total += 1;
            } else if (getChar == 'V') {
                total += 5;
                if (storage == 'I') {
                    total -= 2;
                }
            } else if (getChar == 'X') {
                total += 10;
                if (storage == 'I') {
                    total -= 2;
                }
            } else if (getChar == 'L') {
                total += 50;
                if (storage == 'X') {
                    total -= 20;
                }
            } else if (getChar == 'C') {
                total += 100;
                if (storage == 'X') {
                    total -= 20;
                }
            } else if (getChar == 'D') {
                total += 500;
                if (storage == 'C') {
                    total -= 200;
                }
            } else if (getChar == 'M') {
                total += 1000;
                if (storage == 'C') {
                    total -= 200;
                }
            }

            storage = getChar;
        }

        return total;
    }
}
```

---
### 결과
<img src = "./assets/img/problem-solving/loman-to-integer/result.png"> 

---
### 회고

if문을 사용하고 빼는 값을 단순하게 이전 Symbol을 곱하기 2빼주는 형식으로 코드를 짰는데 이러한 코드 형식은 그다지 관리에 용이하지 않은 것 같다. 

코드를 수정 한다면 Symbol을 딕셔너리로 만들고 관리 할 수 있도록 하고,<br>
문제 조건에 나온 감산법을 각 Symbol에 맞게 Switch문을 만드는게 더 좋을 수도 있을 것 같다.