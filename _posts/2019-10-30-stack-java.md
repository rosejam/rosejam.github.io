---
title: "스택"
date: 2019-10-30T00:10:00-08:00
categories:
  - 자료구조
tags:
  - 스택
  - 자바
  - Reference
---
선형 자료구조.
스택에서는 가장 나중에 삽입된 원소가 삭제된다.
후입선출 = LIFO

스택의 배열 구현
```java
package Data_Structure;

import java.util.Scanner;

class Stack {

    static final int MAX_N = 100; //최대 원소 개수 = MAX_N

    static int top; //top //삽입 및 삭제
    static int stack[] = new int[MAX_N];

    static void stackInit()
    {
        top = -1;
    }

    static boolean stackIsEmpty()
    {
        return (top == -1);
    }

    static boolean stackIsFull()
    {
        return (top == MAX_N - 1);
    }

    static int size()
    {
        return (top + 1);
    }

    static boolean stackPush(int value)
    {
        if (stackIsFull())
        {
            System.out.println("stack overflow!");
            return false;
        }
        
        top++;
        stack[top] = value;

        return true;
    }

    static Integer stackPop()
    {
        if (stackIsEmpty()) 
        {
            System.out.println("stack underflow!");
            return null;
        }
        
        //peek
        Integer value = new Integer(stack[top]);
        
        //remove
        top--;

        return value;
    }

    public static void main(String arg[]) throws Exception {
        Scanner sc = new Scanner(System.in);
        
        int T = sc.nextInt();

        for (int test_case = 1; test_case <= T; test_case++)
        {
            int N = sc.nextInt();

            stackInit();
            for (int i = 0; i < N; i++) 
            {
                int value = sc.nextInt();
                stackPush(value);
            }

            System.out.print("#" + test_case + " ");

            while (!stackIsEmpty())
            {
                Integer value = stackPop();
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
스택 연산은 수행시간이 각각 O(1)이다.

응용 : Function call(재귀호출 등), 깊이우선탐색 DFS

```java
Stack<Integer> stack = new Stack<>();
```
