---
layout: post
title: "[doit자료구조 알고리즘 입문]01-1 반복"
subtitle: "01-1 반복"
categories: study
tags: algorithm
comments: true
---

## 01-2 반복
-----------------------
2. 반복 공부한 내용
- while문 반복 : while(제어식) 명령문
- for문 반복 : for(초기화 부분; 제어식; 업데이트 부분) 명령문
- 양수만 입력하기
- do-while문 반복 : do문 while(제어식)
- 구조적 프로그래밍
- 논리 연산과 드모르간 법칙
- 다중 루프
- 직각 이등변 삼각형 출력

#### 연습문제 Q6
```java
package com.doit.chap01_exam;
import java.util.Scanner;
// 1, 2, …, n의 합을 구합니다.

/**
 * 실습 1-4에서 while문이 종료될 때 변수 i값이 n+1이 됨을 확인하세요
 * (변수 I 값을 출력하도록 프로그램을 수정하세요
 */
class SumWhileEx_01_06 {
	public static void main(String[] args) {
		Scanner stdIn = new Scanner(System.in);

		System.out.println("1부터 n까지의 합을구합니다.");
 		System.out.print("n의 값：");
		int n = stdIn.nextInt();

		int sum = 0;				// 합
		int i = 1;

		while (i <= n) {			// i가 n 이하면 반복합니다.
			sum += i;				// sum에 i를 더합니다.
			i++;					// i 값을 1만큼 증가시킵니다.
		}
		System.out.println("1부터 " + n + "까지의 합은 " + sum + "입니다.");
		System.out.println("i의 값은 " + i + "가(이) 되었습니다.");
	}
}
```

#### 연습문제 Q7
```java
package com.doit.chap01_exam;
import java.util.Scanner;
// 1, 2, …, 7의 합을 구합니다.

/**
 * 실습 1-5 프로그램을 참고하여 n이 7이면 '1+2+3+4+5+6+7=28'로 출력하는 프로그램을 작성하세요
 */
class SumForEx_01_07 {
	public static void main(String[] args) {
		Scanner stdIn = new Scanner(System.in);

		System.out.println("1부터 n까지의 합을 구합니다.");
		System.out.print("n의 값：");
		int n = stdIn.nextInt();

		int sum = 0; // 합

		for (int i = 1; i <= n; i++) {
			if(i < n)
				System.out.print(i + " + ");
			else
				System.out.print(i);
			sum += i; // sum에 i를 더함
		}
		System.out.println(" = " + sum);
	}
}
```

#### 연습문제 Q8
```java
package com.doit.chap01_exam;

import java.util.Scanner;

/**
 *  1부터 10까지의 합은(1+10)*5와 같은 방법으로 구할 수 있습니다.
 *  가우스의 덧셈이라는 방법을 이용하여 1부터 n까지의 정수 합을 구하는 프로그램을 작성하세요.
 */
public class SumGauss_01_08 {
    public static void main(String[] args) {
        Scanner stdIn = new Scanner(System.in);

        System.out.println("1부터 n까지의 합을 구합니다.");
        System.out.print("n의 값：");
        int n = stdIn.nextInt();
        System.out.println("n % 2 = "+n % 2);
        System.out.println((n + 1) +"*"+ (n / 2)+" + "+(n % 2 == 1 ? (n + 1) / 2 : 0));


        int sum = (n + 1) * (n / 2) + (n % 2 == 1 ? (n + 1) / 2 : 0); // 합

        System.out.println("1부터 " + n + "까지의 합은 " + sum + "입니다.");

        //정답과 다른 나의 방법 아래와 같이 곱하기가 먼저되고 2를 나누면 정답과 같음
        int a = 3997;
        sum = ((a + 1) * a)/2;
        System.out.println("sum = "+sum);
    }
}
```

#### 연습문제 Q9
##### 1. 정답
```java
package com.doit.chap01_exam;
import java.util.Scanner;

/**
 * 정수 a.b를 포함하여 그 사이의 모든 정수의 합을 구하여 반환하는 아래의 메서드를 작성하세요.
 */
class SumOf_01_09 {
	static int sumof(int a, int b) {
		int min; // a, b의 작은 쪽의 값
		int max; // a, b의 큰 쪽의 값

		if (a < b) {
			min = a;
			max = b;
		} else {
			min = b;
			max = a;
		}

		int sum = 0; // 합
		for (int i = min; i <= max; i++)
			sum += i;
		return (sum);
	}

	public static void main(String[] args) {
		Scanner stdIn = new Scanner(System.in);

		System.out.println("a와 b를 포함하여 그 사이의 모든 정수의 합을 구합니다.");
		System.out.print("a의 값：");
		int a = stdIn.nextInt();
		System.out.print("b의 값：");
		int b = stdIn.nextInt();

		System.out.println("정수 a, b 사이의 모든 정수의 합은 " + sumof(a, b) + "입니다.");
	}
}
```
##### 2. 내가 푼 방법
```java
package com.doit.chap01_exam;

import java.util.Arrays;

/**
 * 정수 a.b를 포함하여 그 사이의 모든 정수의 합을 구하여 반환하는 아래의 메서드를 작성하세요.
 */
public class SumOf_01_09_my {
    public static void main(String[] args) {

        System.out.println(sumof(120,3));

    }

    static int sumof(int a, int b){
        int[] arr = {a, b};
        Arrays.sort(arr);
        print(arr);
        int sum = 0;
        for (int i =arr[0]; i<= arr[1];i++) {
            sum += i;
        }
        return sum;
    }

    static void print(int[] arr){
        int j=0;
        for(int i : arr){
            System.out.println("arr["+(j++)+"] = "+i);
        }
    }
}
```

#### 연습문제 Q10
##### 1. 정답
```java
package com.doit.chap01_exam;
import java.util.Scanner;
// 정수 b에서 정수 a를 뺀 값을 구합니다(b > a가 되도록 입력 받음)

class Difference_01_10 {
	public static void main(String[] args) {
		Scanner stdIn = new Scanner(System.in);

		System.out.print("a의 값：");
		int a = stdIn.nextInt();

		int b=0;
		while (true) {
			System.out.print("b의 값：");
			b = stdIn.nextInt();
			if (b > a)
				break;
			System.out.println("a보다 큰 값을 입력하세요!");
		}

		System.out.println("b - a는 " + (b - a) + "입니다.");
	}
}
```
##### 2. 내가 푼 방법
```java
package com.doit.chap01_exam;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Scanner;
import java.util.StringTokenizer;

/**
 * 오른쪽과 같이 두 변수 a,b에 정수를 입력하고 b-a를 출력하는 프로그램을 작성하세요
 */
public class Difference_01_10_my {
    public static void main(String[] args) throws IOException {
        System.out.print("a와 b 값을 입력하세요 : ");
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        //공백을 구분자로 값을 읽어 들임
        StringTokenizer st = new StringTokenizer(br.readLine());
        Scanner sc = new Scanner(System.in);

        int a = Integer.parseInt(st.nextToken());
        int b = Integer.parseInt(st.nextToken());
        System.out.println("a의 값 : "+a);
        System.out.println("b의 값 : "+b);

        while (b <= a) {
            System.out.print("a보다 큰 값을 입력하세요 : ");
            b = sc.nextInt();
        }
        System.out.println("b의 값 : "+b);
        System.out.println("b - a는 "+(b-a)+" 입니다.");


    }
}
```

#### 연습문제 Q11
##### 1. 정답
```java
package com.doit.chap01_exam;
import java.util.Scanner;
// 양의 정수값의 자릿수를 구하여 나타냄

class DigitsNo_01_11 {
	public static void main(String[] args) {
		Scanner stdIn = new Scanner(System.in);

		System.out.println("양의 정수값의 자릿수를 구합니다.");

		int n;
		do {
			System.out.print("정수값：");
			n = stdIn.nextInt();
		} while (n <= 0);

		int no = 0; 			// 자릿수
		while (n > 0) {
			n /= 10; 			// n을 10으로 나눔
			System.out.println("n = "+n);
			no++;
		}

		System.out.println("그 수는 " + no + "자리입니다.");
	}
}
```
##### 2. 내가 푼 방법
```java
package com.doit.chap01_exam;

import java.util.Scanner;

/**
 * 양의 정수를 입력하고 자릿수를 출력하는 프로그램을 작성하세요.
 * 예를 들어 135를 입력하면 '그 수는 3자리 입니다.'라고 출력하고, 1314를 입력하면
 * '그 수는 4자리 입니다.'라고 출력하면 됩니다.
 */
public class DigitsNo_01_11_my {
    public static void main(String[] args) {
        System.out.print("양의 정수를 입력하세요 : ");
        Scanner sc = new Scanner(System.in);

        int num = sc.nextInt();
        String val = String.valueOf(num);

        System.out.println(num+"은 "+val.length()+" 자리 입니다.");
    }
}
```

#### 연습문제 Q12
```java
package com.doit.chap01_exam;
// 곱셈표를 출력합니다.

/**
 * 오른쪽과 같이 위쪽과 왼쪽에 곱한느 수가 있는 곱셈푤르 출력하는 프로그램을 작성하세요
 * 구분선은 수직선 기호(|), 마이너스 기호(-), 플러스 기호(+)를 사용하세요
 */
public class Multi99TableEx_01_12 {
	public static void main(String[] args) {
		System.out.print("   |");
		for (int i = 1; i <= 9; i++)
			System.out.printf("%3d", i);
		System.out.println("\n---+---------------------------");

		for (int i = 1; i <= 9; i++) {
			System.out.printf("%2d |", i);
			for (int j = 1; j <= 9; j++)
				System.out.printf("%3d", i * j);
			System.out.println();
		}
	}
}
```

#### 연습문제 Q13
```java
package com.doit.chap01_exam;
// 곱셈표를 출력합니다.

/**
 * 곱셈이 아니라 덧셈을 출력하는 프로그램을 작성하세요
 * 위쪽과 왼쪽에 더하는 수를 출력하세요
 */
public class Add99TableEx_01_13 {
	public static void main(String[] args) {
		System.out.print("   |");
		for (int i = 1; i <= 9; i++)
			System.out.printf("%3d", i);
		System.out.println("\n---+---------------------------");

		for (int i = 1; i <= 9; i++) {
			System.out.printf("%2d |", i);
			for (int j = 1; j <= 9; j++)
				System.out.printf("%3d", i + j);
			System.out.println();
		}
	}
}
```

#### 연습문제 Q14
```java
package com.doit.chap01_exam;

import java.util.Scanner;

/**
 * 오른쪽과 같이 입력한 수를 한 변으로 하는 정사각형을
 *  * 기호로 출력하는 프로그램을 작성하시오
 */
public class Square_01_14 {
    public static void main(String[] args) {
        Scanner sc= new Scanner(System.in);
        int n;

        System.out.println("정사각형 모양으로 나타냅니다.");

        do {
            System.out.print("단수는：");
            n = sc.nextInt();
        } while (n <= 0);

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++)
                System.out.print("*");
            System.out.println();
        }

    }
}
```

#### 연습문제 Q15
##### 1. 정답
```java
package com.doit.chap01_exam;
import java.util.Scanner;
// 4가지의 직각삼각형 모양으로 나타냄

public class Triangle_01_15 {
	// 왼쪽 아래가 직각인 이등변삼각형을 출력
	static void triangleLB(int n) {
		for (int i = 1; i <= n; i++) { 				// i행 (i = 1, 2, … ,n)
			for (int j = 1; j <= i; j++) 			// i개의 '*'를 나타냄
				System.out.print('*');
			System.out.println(); 					// 개행(줄변환)
		}
	}

	// 왼쪽 위가 직각인 이등변삼각형을 출력
	static void triangleLU(int n) {
		for (int i = 1; i <= n; i++) { 				// i행 (i = 1, 2, … ,n)
			for (int j = 1; j <= n - i + 1; j++) 	// n-i+1개의 '*'를 나타냄
				System.out.print('*');
			System.out.println(); 					// 개행(줄변환)
		}
	}

	// 오른쪽 위가 직각인 이등변삼각형을 출력
	static void triangleRU(int n) {
		for (int i = 1; i <= n; i++) { 				// i행 (i = 1, 2, … ,n)
			for (int j = 1; j <= i - 1; j++) 		// i-1개의 ' '를 나타냄
				System.out.print(' ');
			for (int j = 1; j <= n - i + 1; j++) 	// n-i+1개의 '*'를 나타냄
				System.out.print('*');
			System.out.println();					// 개행(줄변환)
		}
	}

	// 오른쪽 아래가 직각인 이등변삼각형을 출력
	static void triangleRB(int n) {
		for (int i = 1; i <= n; i++) { 				// i행 (i = 1, 2, … ,ln)
			for (int j = 1; j <= n - i; j++) 		// n-i개의 ' '를 나타냄
				System.out.print(' ');
			for (int j = 1; j <= i; j++) 			// i개의 '*'를 나타냄
				System.out.print('*');
			System.out.println(); 					// 개행(줄변환)
		}
	}

	public static void main(String[] args) {
		Scanner stdIn = new Scanner(System.in);
		int n;

		System.out.println("삼각형 모양으로 나타냅니다.");

		do {
			System.out.print("단수는 ：");
			n = stdIn.nextInt();
		} while (n <= 0);

		System.out.println("왼쪽 아래가 직각인 삼각형");
		triangleLB(n); // 왼쪽 아래가 직각인 이등변삼각형

		System.out.println("왼쪽 위가 직각인 삼각형");
		triangleLU(n); // 왼쪽 위가 직각인 이등변삼각형

		System.out.println("오른쪽 위가 직각인 삼각형");
		triangleRU(n); // 오른쪽 위가 직각인 이등변삼각형

		System.out.println("오른쪽 아래가 직각인 삼각형");
		triangleRB(n); // 오른쪽 아래가 직각인 이등변삼각형
	}
}
```
##### 2. 내가 푼 방법
```java
package com.doit.chap01_exam;
import java.util.Scanner;
// 왼쪽 아래가 직각인 이등변 삼각형을 출력합니다.

public class Triangle_01_15_my {
	public static void main(String[] args) {
		Scanner stdIn = new Scanner(System.in);
		int n;
		System.out.println("왼쪽 아래가 직각인 이등변 삼각형을 출력합니다.");
		do {
			System.out.print("몇 단 삼각형입니까? : ");
			n = stdIn.nextInt();
		} while (n <= 0);

		triangleLB(n);
		System.out.println();
		triangleLU(n);
		System.out.println();
		triangleRU(n);
		System.out.println();
		triangleRB(n);
	}

	//왼쪽 아래가 직각인 이등변 삼각형을 출력
	static void triangleLB(int n){

		for (int i = 1; i <= n; i++){
			for (int j = 1; j <= i; j++) 
				System.out.print('*');
			System.out.println();
		}
	}
	//왼쪽 위가 직각인 이등변 삼각형을 출력
	static void triangleLU(int n){

		for (int i = n; i > 0; i--){
			for (int j = i; j > 0; j--) 
				System.out.print('*');
			System.out.println();
		}
	}
	//오른쪽 위가 직각인 이등변 삼각형을 출력
	static void triangleRU(int n){
		for (int i = n; i > 0; i--){
			for (int s = 0; s < (n-i); s++)
				System.out.print(" ");
			for (int j = i; j > 0; j--)
				System.out.print("*");
			System.out.println();
		}
	}
	//오른쪽 아래가 직각인 이등변 삼각형을 출력
	static void triangleRB(int n){
		for (int i = 1; i <= n; i++){
			for (int s = 0; s < (n-i); s++)
				System.out.print(" ");
			for (int j = 1; j <= i; j++)
				System.out.print("*");
			System.out.println();
		}
	}
}
```

#### 연습문제 Q16
##### 1. 정답
```java
package com.doit.chap01_exam;
import java.util.Scanner;
// 기호문자 *로 피라미드를 출력함

class StarPira_01_16 {

	static void spira(int n) {
		for (int i = 1; i <= n; i++) { 					// i행 (i = 1, 2, … ,n)
			for (int j = 1; j <= n - i + 1; j++) 		// n-i+1개의 ' '를 나타냄
				System.out.print(' ');
			for (int j = 1; j <= (i - 1) * 2 + 1; j++) 	// (i-1)*2+1개의 '*'를 나타냄
				System.out.print('*');
			System.out.println(); 						// 개행(줄변환)
		}
	}

	public static void main(String[] args) {
		Scanner stdIn = new Scanner(System.in);
		int n;

		System.out.println("피라미드 모양으로 나타냅니다.");

		do {
			System.out.print("단수는 ：");
			n = stdIn.nextInt();
		} while (n <= 0);

		spira(n); 		// 피라미드를 나타냄
	}
}
```
##### 2. 내가 푼 방법
```java
package com.doit.chap01_exam;

import java.util.Scanner;

/**
 * n단의 피라미드를 출력하는 메서드를 작성하세요
 */
public class StarPira_01_16_my {
    public static void main(String[] args) {

        System.out.print("n 값을 입력하세요 : ");
        Scanner sc= new Scanner(System.in);
        int n = sc.nextInt();
        spira(n);
    }

    static void spira(int n){
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n - i; j++) 
                System.out.print(" ");
            for (int j = 0; j <= i; j++) 
                System.out.print("*");
            for (int j = 1; j <= i ; j++) 
                System.out.print("*");
            System.out.println();
        }
    }
}
```

#### 연습문제 Q17
##### 1. 정답
```java
package com.doit.chap01_exam;
import java.util.Scanner;
// 숫자를 늘어놓아 피라미드를 출력

class NumPira_01_17 {
	static void npira(int n) {
		for (int i = 1; i <= n; i++) { 					// i행 (i = 1, 2, … ,n)
			for (int j = 1; j <= n - i + 1; j++) 		// n-i+1개의 ' '를 나타냄
				System.out.print(' ');
			for (int j = 1; j <= (i - 1) * 2 + 1; j++) 	// (i-1)*2+1개의 '*'를 나타냄
				System.out.print(i % 10);
			System.out.println(); 						// 개행(줄변환)
		}
	}

	public static void main(String[] args) {
		Scanner stdIn = new Scanner(System.in);
		int n;

		System.out.println("피라미드 모양으로 나타냅니다.");

		do {
			System.out.print("단수는 ：");
			n = stdIn.nextInt();
		} while (n <= 0);

		npira(n); // 피라미드를 나타냄
	}
}
```
##### 2. 내가 푼 방법
```java
package com.doit.chap01_exam;

import java.util.Scanner;

/**
 * 아래를 향한 n단의 숫자 피라미드를 출력하는 메서드를 작성하세요
 */
public class NumPira_01_17_my {
    public static void main(String[] args) {
        System.out.println("n값을 입력하세요 : ");
        Scanner sc= new Scanner(System.in);
        int n= sc.nextInt();
        npira(n);

    }

    static void npira(int n){
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j < n - i+1; j++) 
                System.out.print(" ");
            for (int j = 1; j <= i; j++) 
                System.out.print(i);
            for (int j = 2; j <= i; j++) 
                System.out.print(i);
            System.out.println();
        }
    }
}
```