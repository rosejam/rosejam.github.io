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

public class Main {
	public static StringBuilder sb;
	public static StringTokenizer st;
	public static int N, M, V, s, e;
	public static int visit[]; // 방문처리는 1번씩 모두 true로 체크하고 끝난다.
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
//			graph[temp1][temp2] = graph[temp2][temp1] = 1;
//		}

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

		sb = new StringBuilder();

		DFSB(V);
		//
//		visit = new int[N + 1];
//		DFSR(V);
//		sb.append('\n');

		BFSB(V);

		bw.write(sb.toString());
		bw.flush();
	}

	private static void DFSA(int vertex) {
		visit = new int[N + 1];
		stack = new Stack<>();
		stack.push(vertex);
		while (!stack.isEmpty()) {
			vertex = stack.pop();
			if (visit[vertex] == 0) {
				visit[vertex] = 1;
				sb.append(vertex).append(' ');
//				for (int i = N; i >= 1; i--) {
//					if (graph[vertex][i] == 1 && visit[i] == 0) {
//						stack.push(i);
//					}
//				}
				for (int i = graph[vertex].size() - 1; i >= 0; i--) {
					int tmp = graph[vertex].get(i);
					if (visit[tmp] == 0) {
						stack.push(tmp);
					}
				}
			}
		}
		sb.append('\n');
	}

	private static void DFSB(int vertex) {
		visit = new int[N + 1];
		stack = new Stack<>();
		visit[vertex] = 1;
		sb.append(vertex).append(' ');
		stack.push(vertex);
		while (!stack.isEmpty()) {
//			boolean flag = false;//
//			vertex = stack.peek();//
			vertex = stack.pop();//
			for (int i = 0; i < graph[vertex].size(); i++) {
				int tmp = graph[vertex].get(i);
				if (visit[tmp] == 0) {
					stack.push(vertex);//
					visit[tmp] = 1;
					sb.append(tmp).append(' ');
					stack.push(tmp);
//					flag = true;//
					break;////
				}
			}
//			if (!flag) {//
//				stack.pop();//
//			}
		}
		sb.append('\n');
	}

	private static void DFSR(int vertex) {
		visit[vertex] = 1;
		sb.append(vertex).append(' ');
		for (int i = 0; i < graph[vertex].size(); i++) {
			int tmp = graph[vertex].get(i);
			if (visit[tmp] == 0) {
				DFSR(tmp);
			}
		}
	}

	private static void BFSA(int vertex) {
		visit = new int[N + 1];
		queue = new LinkedList<>();
		queue.add(vertex);
		while (!queue.isEmpty()) {
			vertex = queue.remove();
			if (visit[vertex] == 0) {
				visit[vertex] = 1;
				sb.append(vertex).append(' ');
//				for (int i = 1; i <= N; i++) {
//					if (graph[vertex][i] == 1 && visit[i] == 0) {
//						queue.add(i);
//					}
//				}
				for (int i = 0; i < graph[vertex].size(); i++) {
					int tmp = graph[vertex].get(i);
					if (visit[tmp] == 0) {
						queue.add(tmp);
					}
				}
			}
		}
		sb.append('\n');
	}

	private static void BFSB(int vertex) {
		visit = new int[N + 1];
		queue = new LinkedList<>();
		visit[vertex] = 1;
		sb.append(vertex).append(' ');//
		queue.add(vertex);
		while (!queue.isEmpty()) {
			vertex = queue.remove();
//			sb.append(vertex).append(' ');//
			for (int i = 0; i < graph[vertex].size(); i++) {
				int tmp = graph[vertex].get(i);
				if (visit[tmp] == 0) {
					visit[tmp] = 1;
					sb.append(tmp).append(' ');//
					queue.add(tmp);
				}
			}
		}
		sb.append('\n');
	}

}

```

