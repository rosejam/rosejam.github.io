---
title: "DFS와 BFS"
date: 2021-01-12T00:12:00-09:00
categories:
  - PS
tags:
  - 백준
  - DFS
  - BFS
  - 자바
---

```java
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.util.ArrayList;
import java.util.Collections;
import java.util.LinkedList;
import java.util.Queue;
import java.util.Stack;
import java.util.StringTokenizer;

public class Main_BJ_1260_DFS와BFS {
	public static StringBuilder sb;
	public static StringTokenizer st;
	public static int N, M, V, s, e;
	public static boolean visit[], flag; // 방문처리는 "1번씩 모두" true로 체크하고 끝난다.
	public static ArrayList<Integer> graph[];
	public static Stack<Integer> stack;
	public static Queue<Integer> queue;

	public static void main(String[] args) throws Exception {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

		st = new StringTokenizer(br.readLine(), " ");

		N = Integer.parseInt(st.nextToken());
		M = Integer.parseInt(st.nextToken());
		V = Integer.parseInt(st.nextToken());

//		// 인접행렬방식
//		graph = new int[N + 1][N + 1];
//		for (int m = 0; m < M; m++) {
//			st = new StringTokenizer(br.readLine(), " ");
//			s = Integer.parseInt(st.nextToken());
//			e = Integer.parseInt(st.nextToken());
//			// 두 점 사이 여러개의 간선이 있을 수 있음, 간선은 양방향
//			graph[s][e] = graph[e][s] = 1;
//		}
		//
		// 인접 리스트 방식
		graph = new ArrayList[N + 1];
		for (int n = 1; n <= N; n++) {
			graph[n] = new ArrayList<>();
		}
		for (int m = 1; m <= M; m++) {
			st = new StringTokenizer(br.readLine(), " ");
			s = Integer.parseInt(st.nextToken());
			e = Integer.parseInt(st.nextToken());
			// 두 점 사이 여러개의 간선이 있을 수 있음, 간선은 양방향
			graph[s].add(e);
			graph[e].add(s);
		}
		for (int n = 1; n <= N; n++) {
			Collections.sort(graph[n]);
		}
		//
		
		sb = new StringBuilder();

		visit = new boolean[N + 1];
		DFSB(V);
		
		sb.append('\n');

		visit = new boolean[N + 1];
		BFSB(V);

		bw.write(sb.toString());
		bw.flush();
	}

	private static void DFSA(int vertex) {
		stack = new Stack<>();
		stack.push(vertex);
		while (!stack.isEmpty()) {
			vertex = stack.pop();
			if (!visit[vertex]) {
				visit[vertex] = true;
				sb.append(vertex).append(' ');
//				//인접행렬방식
//				for (int i = N; i >= 1; i--) {
//					if (graph[vertex][i] == 1 && !visit[i]) {
//						stack.push(i);
//					}
//				}
				for (int i = graph[vertex].size() - 1; i >= 0; i--) {
					int tmp = graph[vertex].get(i);
					if (!visit[tmp]) {
						stack.push(tmp);
					}
				}
			}
		}
	}

	private static void DFSB(int vertex) {
		stack = new Stack<>();
		visit[vertex] = true;
		sb.append(vertex).append(' ');
		stack.push(vertex);
		while (!stack.isEmpty()) {
//			flag = false;//경우2
//			vertex = stack.peek();//경우2
			vertex = stack.pop();//경우1
			for (int i = 0; i < graph[vertex].size(); i++) {
				int tmp = graph[vertex].get(i);
				if (!visit[tmp]) {
					stack.push(vertex);//경우1 //여기서 추가로 i++을 저장하면 좋다.
					visit[tmp] = true;
					sb.append(tmp).append(' ');
					stack.push(tmp);
//					flag = true;//경우2
					break;/*중요*/
				}
			}
//			if (!flag) {//경우2
//				stack.pop();//경우2
//			}//경우2
		}
	}

	private static void DFSR(int vertex) {
		visit[vertex] = true;
		sb.append(vertex).append(' ');
		for (int i = 0; i < graph[vertex].size(); i++) {
			int tmp = graph[vertex].get(i);
			if (!visit[tmp]) {
				DFSR(tmp);
			}
		}
	}

	private static void BFSA(int vertex) {
		queue = new LinkedList<>();
		queue.add(vertex);
		while (!queue.isEmpty()) {
			vertex = queue.remove();
			if (!visit[vertex]) {
				visit[vertex] = true;
				sb.append(vertex).append(' ');
//				//인접행렬방식
//				for (int i = 1; i <= N; i++) {
//					if (graph[vertex][i] == 1 && !visit[i]) {
//						queue.add(i);
//					}
//				}
				for (int i = 0; i < graph[vertex].size(); i++) {
					int tmp = graph[vertex].get(i);
					if (!visit[tmp]) {
						queue.add(tmp);
					}
				}
			}
		}
	}

	private static void BFSB(int vertex) {
		queue = new LinkedList<>();
		visit[vertex] = true;
		sb.append(vertex).append(' ');//경우1
		queue.add(vertex);
		while (!queue.isEmpty()) {
			vertex = queue.remove();
//			sb.append(vertex).append(' ');//경우2
			for (int i = 0; i < graph[vertex].size(); i++) {
				int tmp = graph[vertex].get(i);
				if (!visit[tmp]) {
					visit[tmp] = true;
					sb.append(tmp).append(' ');//경우1
					queue.add(tmp);
				}
			}
		}
	}

}

```

