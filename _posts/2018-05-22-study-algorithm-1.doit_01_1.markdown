---
layout: post
title: "[doit자료구조 알고리즘 입문]01-1 알고리즘이란?"
subtitle: "01-1 알고리즘이란?"
categories: study
tags: algorithm
comments: true
---

## 01-1 알고리즘이란?
-------------------------
### 알고리즘이란?
	문제를 해결하기 위한 것으로, 명확하게 정의되고 순서가 있는 유한 개의 규칙으로 이루어진 집합

1. 알고리즘이란 공부내용
- 간단한 JAVA 키보드로 숫자와 문자열 입력하기 
- 매개변수
- 메서드의 반환값과 메서드호출식의 평가
- 세 값의 대소 관계와 중앙값
-  조건 판단과 분기
-  연산자와 피연산자
		- 단항 연산자
		- 2항 연산자
		- 3항 연산자
-  순서도의 기호
		- 프로그램 순서도
		- 데이터
		- 처리
		- 미리 정의한 처리
		- 판단
		- 루프 범위
		- 선
			- 실선
			- 점선
			- 파선
		- 단말

#### 연습문제 Q1
```java
package com.doit.chap01_exam;

/**
 * 네 값의 최대값을 구하는 max4 메서드를 작성하세요
 */
public class Max4_01_01 {
    public static void main(String[] args) {

        System.out.println("max4(4,3,2,1) = " + max4(4, 3, 2, 1)); // [A] a＞b＞c＞d

    }

    /**
     * 네 값의 최대값을 구하는 max4 메서드
     * @param a
     * @param b
     * @param c
     * @param d
     * @return
     */
    static int max4(int a, int b, int c, int d){
        int max = a;
        if(b > max)
            max = b;
        if(c > max)
            max = c;
        if(d > max)
            max = d;

        //구한 최대값을 호출한 곳으로 반환
        return max;
    }

}

```
#### 연습문제 Q2
```java
package com.doit.chap01_exam;

/**
 * 세 값의 최소값을 구하는 min3 메서드를 작성하세요
 */
public class Min3_01_02 {
    public static void main(String[] args) {

        System.out.println("min3(3,2,1) = " + min3(3, 2, 1));

    }

    /**
     * 세 값의 최소값을 구하는 min3 메서드를 작성하세요
     * @param a
     * @param b
     * @param c
     * @return
     */
    static int min3(int a, int b, int c){
        int min = a;
        if(b < min)
            min = b;
        if(c < min)
            min = c;

        //구한 최소값을 호출한 곳으로 반환
        return min;
    }

}
```
#### 연습문제 Q3
```java
package com.doit.chap01_exam;

/**
 * 네 값의 최소값을 구하는 min4 메서드를 작성하세요
 */
public class Min4_01_03 {
    public static void main(String[] args) {

        System.out.println("min4(4,3,2,1) = " + min4(4, 3, 2, 1));

    }

    /**
     * 네 값의 최소값을 구하는 min4 메서드
     * @param a
     * @param b
     * @param c
     * @param d
     * @return
     */
    static int min4(int a, int b, int c, int d){
        int min = a;
        if(b < min)
            min = b;
        if(c < min)
            min = c;
        if (d < min)
            min = d;

        //구한 최소값을 호출한 곳으로 반환
        return min;
    }

}

```

#### 연습문제 Q4
```java
package com.doit.chap01_exam;

/**
 * 세 값의 대소 관계 13종류의 모든 조합에 대해 중앙값을 구하여 출력하는 프로그램을 작성하세요
 */
public class Med3_01_04 {
    public static void main(String[] args) {
        System.out.println("med3(3,2,1) = " + med3(3, 2, 1)); // [A] a＞b＞c
        System.out.println("med3(3,2,2) = " + med3(3, 2, 2)); // [B] a＞b＝c
        System.out.println("med3(3,1,2) = " + med3(3, 1, 2)); // [C] a＞c＞b
        System.out.println("med3(3,2,3) = " + med3(3, 2, 3)); // [D] a＝c＞b
        System.out.println("med3(2,1,3) = " + med3(2, 1, 3)); // [E] c＞a＞b
        System.out.println("med3(3,3,2) = " + med3(3, 3, 2)); // [F] a＝b＞c
        System.out.println("med3(3,3,3) = " + med3(3, 3, 3)); // [G] a＝b＝c
        System.out.println("med3(2,2,3) = " + med3(2, 2, 3)); // [H] c＞a＝b
        System.out.println("med3(2,3,1) = " + med3(2, 3, 1)); // [I] b＞a＞c
        System.out.println("med3(2,3,2) = " + med3(2, 3, 2)); // [J] b＞a＝c
        System.out.println("med3(1,3,2) = " + med3(1, 3, 2)); // [K] b＞c＞a
        System.out.println("med3(2,3,3) = " + med3(2, 3, 3)); // [L] b＝c＞a
        System.out.println("med3(1,2,3) = " + med3(1, 2, 3)); // [M] c＞b＞a
    }

    static int med3(int a, int b, int c) {
        if (a >= b)
            if(b >= c)
                return b;
            else if (a <= c)
                return a;
            else
                return c;
        else if(a > c)
            return a;
        else if(b > c)
            return c;
        else
            return b;
    }
}
```

#### 연습문제 Q5
```java
package com.doit.chap01_exam;

import java.util.Scanner;

/**
 * 3개의 정수값을 입력하고 중앙값을 구한 다음 출력합니다
 *
 * 연습1-5 해답
 * 가장 처음의 if문의 판단
 * if ((b >= a && c<= a) || (b <= a && c >= a))
 * 에 주목합니다. 여기서 b >= a 및 b <= a의 판단을 뒤집은 판단(실질적으로 같은 판단)을 이어지는 else 이후의
 * else if ((a > b && c < b) || (b <= a && c > b))
 * 으로 수행합니다. 결국 가장 처음의 if가 성립한 경우 2 번째의 if에서도 (실질적으로)같은 판단을 수행하므로 효율이 나빠집니다.
 */

public class Practice_01_05 {
    public static void main(String[] args) {
        Scanner stdIn = new Scanner(System.in);

        System.out.println("세 정수의 중앙값을 구합니다.");
        System.out.print("a의 값 : ");
        int a = stdIn.nextInt();
        System.out.print("b의 값 : ");
        int b = stdIn.nextInt();
        System.out.print("c의 값 : ");
        int c = stdIn.nextInt();

        System.out.println("중앙값은 " +med3(a, b, c) + "입니다.");
    }

    static int med3(int a, int b, int c) {
        if ((b >= a && c<= a) || (b <= a && c >= a))
            return a;
        else if ((a > b && c < b) || (b <= a && c > b))
            return b;
        return c;
    }

}
```