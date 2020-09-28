---
title: "큐"
date: 2019-10-30T00:10:00-09:00
categories:
  - 자료구조
tags:
  - 큐
  - 자바
  - Reference
---
선형 자료구조.
큐에서는 가장 먼저 삽입된 원소가 삭제된다.
선입선출 = FIFO

원형큐의 배열 구현
```java
package Data_Structure;

import java.util.Scanner;

class Queue {

    static final int MAX_N = 100; //최대 원소 개수 + 1

    static int rear; //tail //삽입
  	static int front; //head //삭제
    static int queue[] = new int[MAX_N];

    static void queueInit()
    {
      	rear = 0;
        front = 0;
    }

    static boolean queueIsEmpty()
    {
        return (rear == front);
    }

    static boolean queueIsFull()
    {
        return ((rear + 1) % MAX_N == front);
    }

    static boolean queueEnqueue(int value)
    {
        if (queueIsFull())
        {
            System.out.print("queue overflow!");
            return false;
        }
      	
        queue[rear] = value;
        rear++;
        if (rear == MAX_N)
        {
            rear = 0;
        }
        
        return true;
    }

    static Integer queueDequeue()
    {
        if (queueIsEmpty()) 
        {
            System.out.print("queue underflow!");
            return null;
        }
        
        //peek
        Integer value = new Integer(queue[front]);
        
        //delete
        front++;
        if (front == MAX_N)
        {
            front = 0;
        }
        
        return value;
    }

    public static void main(String arg[]) throws Exception {
        Scanner sc = new Scanner(System.in);
        
        int T = sc.nextInt();

        for (int test_case = 1; test_case <= T; test_case++)
        {
            int N = sc.nextInt();

            queueInit();
            for (int i = 0; i < N; i++)
            {
                int value = sc.nextInt();
                queueEnqueue(value);
            }

            System.out.print("#" + test_case + " ");
            
            while (!queueIsEmpty())
            {
                Integer value = queueDequeue();
                if (value != null)
                {
                    System.out.print(value.intValue() + " ");
                }
            }
            System.out.println();
        }
        sc.close();
    }
}
```
각 연산은 수행시간이 각각 O(1)이다.

응용 : Buffer, 너비우선탐색 BFS

```java
Queue<Integer> queue = new LinkedList<>();
```
