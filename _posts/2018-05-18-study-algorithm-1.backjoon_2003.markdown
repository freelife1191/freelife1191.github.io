---
layout: post
title: "[BAEKJOON]2003 Python 및 Java 풀이"
subtitle: "2003 수들의 합 2 - 투포인터"
categories: study
tags: algorithm
comments: true
---

## 백준 2003 수들의 합2 문제 풀이
-------------------
문제 링크 : https://www.acmicpc.net/problem/2003

투포인터 알고리즘을 이용해 N개의 1차원 배열의 합이 M이 되는 횟수를 구하는 문제

### Python3 풀이
```python
'''
문제는 투포인터를 이용해 두개의 포인터의 합이 M이 되는 횟수를 카운트를 세는 것임
N개의 1차원 배열이 있고 N의 배열만큼 첫번째 포인터 루프문을 돌면서 sum에 부분배열 값을 더함
sum >= M 이면 sum < M 이 될때까지 두번째 포인터 루프문을 돌면서 sum에 두번째 포인터 부분배열 값을 뺌
이렇게 진행하면서 sum == M인 순간에 횟수 카운트 r을 증가시킴
'''
r=0 #결과값
sum=0 #합계
s=0 #첫번째 포인터
N,M = [int(x) for x in input().split()]  #N과 M값을 입력받음
data = [int(x) for x in input().split()] #N 만큼의 데이터 입력받음
for x in data: #배열 만큼 루프 돔
    sum += x #합계에 현재 부분배열 값을 더함
    if sum >= M: #합계가 M보다 크거나 같으면 조건식 시작
        while sum >= M: #합계가 M보다 크가나 같으면 루프
            if sum == M: #합계와 M이 같으면
                r += 1 #결과값 카운트 1 증가
            sum -= data[s] #두번째 포인터의 부분배열을 증가시키면서 값을 뺀다
            s += 1 #두번째 포인터 배열 증가
print(r)
```

### Java 풀이
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.StringTokenizer;

public class bj2003 {

    static int n, m;

    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        n = Integer.parseInt(st.nextToken());
        m = Integer.parseInt(st.nextToken());

        st = new StringTokenizer(br.readLine());

        ArrayList<Integer> list = new ArrayList<Integer>();
        for (int i = 0; i < n; i++) {
            list.add(Integer.parseInt(st.nextToken()));
        }

        int count = 0;
        int sum = 0;
        int i = 0, j = 0; // i = 시작점, j = 끝점
        while (true) {
            if(sum >= m) {
                sum -= list.get(j++);
            } else if (i == n){
                break;
            } else {
                sum += list.get(i++);
            }
            if(sum == m){
                count++;
            }
        }
        System.out.println(count);
    }
}

```