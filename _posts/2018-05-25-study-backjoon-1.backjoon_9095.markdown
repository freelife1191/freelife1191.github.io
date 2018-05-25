---
layout: post
title: "[BAEKJOON]9095(1, 2, 3 더하기) Python 및 Java 풀이"
subtitle: "9095 1, 2, 3 더하기 - 다이나믹 프로그래밍"
categories: study
tags: backjoon
comments: true
---

## 백준 9095 1, 2, 3 더하기 문제 풀이
-------------------
문제 링크 : https://www.acmicpc.net/problem/9095

정수 `n`이 주어졌을 때, `n`을 **1,2,3**의 합으로 나타내는 방법의 수를 구하는 문제

각 케이스 마다 `n`을 **1,2,3**의 합으로 나타내기 위해
최초 예시에 이미 나와있는 **1,2,3**의 **경우의 수** **1,2,4** 를 리스트에 입력하고
루프문으로 `n`값 만큼 증가시키면서 `n-1`, `n-2`, `n-3` 값을 계속 합산하여
최종 `n`값의 경우의 수를 만들어낸다

### Python3 풀이
```python
#l = [4,7,10] #n 값을 받은 리스트
l=[]
#입력받은 T갯수 만큼 돌면서 n값을 입력받아 리스트에 append 시킨다
for T in range(int(input())): #갯수 T 입력
    l.append(int(input()))    #n 값 입력

#리스트에 받은 n값 중 최대값을 k에 대입한다
k = max(l)
#입력받은 n의 최대값이 11미만이고 0보다 클때만 수행한다
if k >= 0 and k < 11:
    #사전에 계산된 0,1,2,3에 대한 경우의 수 리스트를 미리 생성한다
    m = [0,1,2,4]
    '''
    경우의 수에 이미 4개의 값이 있으므로 n의 최대값에서 -3을 한 값을
    range에 대입하여 루프문을 돌린다
    range의 값은 입력된값의 미만까지 구하므로 결국 리스트에서 4개의 값을 제외한것이다
    '''
    for i in range(k-3):
        '''
        상위 n값의 경우의 수는 n-1, n-2, n-3 의 경우의 수를 더한 값과 같으므로
        리스트의 가장 마지막 경우의 수 세개를 더하면 상위 경우의 수가 계산되며
        계산된 경우의 수를 리스트에 append한다
        '''
        m.append(m[-1]+m[-2]+m[-3])

    for i in l:
        print(m[i])
else :
    print('k값 오류')
```

### Java 풀이
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        int[] arr = new int[11];
        int T, n;
        Scanner scanner = new Scanner(System.in);

        arr[0] = 0; // 정수가 0일 때 방법(경우)의 수
        arr[1] = 1; // 정수가 1일 때 경우의 수, 1 => 1개
        arr[2] = 2; // 정수가 2일 때 경우의 수, 1+1, 2 => 2개
        arr[3] = 4; // 정수가 3일 때 경우의 수, 1+1+1, 1+2, 2+1, 3 => 4개
        T = scanner.nextInt();
        for(int i = 0; i < T; i++) {
            n = scanner.nextInt();
            for(int j = 4; j <= n; j++){
                arr[j] = arr[j-1] + arr[j-2] + arr[j-3];
            }
            System.out.println(arr[n]);
        }
        scanner.close();
    }
}
```