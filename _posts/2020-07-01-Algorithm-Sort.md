---
title: "[Algorithm] 기본 정렬 알고리즘"
date: 2020-07-01
categories:
  - blog
tags:
  - Java
  - Algorithm
comments: true
excerpt: 
last_modified_at: 2020-07-01
toc: true
---

## 1-1. 기본 정렬 알고리즘(Sort Algorithm)

- 1. Bubble Sort
- 2. Insertion Sort
- 3. Selection Sort


### 1. Selection Sort

(1) 각 루프마다 최대 원소를 찾는다.
(2) 최대 원소와 맨 오른쪽 원소를 교환한다.
(3) 맨 오른쪽 원소를 제외한다.
(4) 하나의 원소만 남을 때까지 (1~3) 루프를 반복한다.


#### pseudocode

```java
selectionSort(Array, n){
	for last <- n downto 2{
		array 중 가장 큰 수 array[i]를 찾음
		array[i] <-> array[last]; array[i]와 array[last] 값을 교환
	}
}
```

```java
public class SelectionSort {
	private static int[] arr = { 8, 21, 2, 4, 42, 11 };

	public static void main(String[] args) {
		selectionSortMin(arr, arr.length);
		for (int a : arr) {
			System.out.print(a + " ");
		}
		System.out.println();

		selectionSortMax(arr, arr.length);
		for (int b : arr) {
			System.out.print(b + " ");
		}
	}
	
	// 오름차순 정렬
	private static void selectionSortMin(int[] arr, int length) {
		int min;	// 최소값의 인덱스 번호 저장
		int tmp;	// 2개의 숫자 대소 비교 후 자리를 바꾸기 위해 임시로 넣어줄 변수

		for (int i = 0; i < length; i++) {
			min = i;

			for (int j = i + 1; j < length; j++) {	// min번지 값과 다른 숫자들을 반복문을 돌며 비교
				if (arr[j] < arr[min]) {			// min번지 값보다 작은 값이 있으면 min = j 로 바꿔준다
					min = j;
				}
			}

			tmp = arr[i];		// i번지 값을 임시로 tmp에 넣어준다
			arr[i] = arr[min];	// i번지 값을 min번지 값으로 바꿔준다
			arr[min] = tmp;		// min번지에는 tmp의 값을 넣어준다
		}
	}

	// 내림차순 정렬
	private static void selectionSortMax(int[] arr, int length) {
		int max;
		int tmp;

		for (int i = 0; i < length; i++) {
			max = i;
			for (int j = i + 1; j < length; j++) {
				if (arr[j] > arr[max]) {
					max = j;
				}
			}
			tmp = arr[i];
			arr[i] = arr[max];
			arr[max] = tmp;
		}
	}
}
```



### 2. Bubble Sort


(1) 1의 for 루프는 n-1번 반복
(2) 2의 for 루프는 각각 n-1, n-2, ..., 2, 1번 반복
(3) 3에서 교환


#### pseudocode

```java
bubbleSort(arr[], n){
	for last <- downto 2 {		// 1
		for i <- to last-1		// 2
		if(arr[i] > arr[i+1]) arr[i] <-> arr[i+1]  // 3
	}
}
```


```java
public class BubbleSort {
	private static int[] arr = { 8, 21, 2, 4, 42, 11 };

	public static void main(String[] args) {
		bubbleSortAsc(arr, arr.length);
		for (int a : arr) {
			System.out.print(a + " ");
		}
		System.out.println();
		
		bubbleSortDes(arr, arr.length);
		for (int a : arr) {
			System.out.print(a + " ");
		}
	}
	
	//오름차순 정렬
	private static void bubbleSortAsc(int[] arr, int length) {
		int tmp;
		
		for (int i = length - 1; i > 0; i--) {	// 2개 값 비교해서 가장 큰수는 배열 마지막 번지에 넣어준다
			for (int j = 0; j < i; j++) {		
				if (arr[j] > arr[j + 1]) {
					tmp = arr[j];
					arr[j] = arr[j + 1];
					arr[j + 1] = tmp;
				}
			}
		}
	}
	
	//내림차순 정렬
	private static void bubbleSortDes(int[] arr, int length) {
		int tmp;
		
		for (int i = length - 1; i > 0; i--) {
			for (int j = 0; j < i; j++) {
				if (arr[j] < arr[j + 1]) {
					tmp = arr[j];
					arr[j] = arr[j + 1];
					arr[j + 1] = tmp;
				}
			}
		}
	}
}
```




### 3. Insertion Sort


(1) 배열의 모든 원소를 앞에서부터 차례대로 이미 정렬된 배열 부분과 비교한다.
(2) 비교를 한 뒤 삽입할 위치를 지정한다.
(3) 지정된 위치의 원래 원소는 뒤로 옮기고 지정한 자리에 원소를 삽입한다.

#### pseudocode

```java
insertionSort(arr[], n){
	for i <- 2 to n
	arr[1...i]의 적당한 자리에 arr[i] 삽입
	}
```


```java
public class InsertionSort {
	private static int[] arr = { 8, 21, 2, 4, 42, 11 };

	public static void main(String[] args) {
		insertionSortAsc(arr, arr.length);
		for (int a : arr) {
			System.out.print(a + " ");
		}
		System.out.println();
		insertionSortDes(arr, arr.length);
		for (int b : arr) {
			System.out.print(b + " ");
		}
	}

	private static void insertionSortAsc(int[] arr, int length) {
		int tmp;

		for (int i = 1; i < length; i++) {
			for (int j = i; j > 0; j--) {
				if (arr[j - 1] > arr[j]) {
					tmp = arr[j - 1];
					arr[j - 1] = arr[j];
					arr[j] = tmp;
				}
			}
		}
	}

	private static void insertionSortDes(int[] arr, int length) {
		int tmp;

		for (int i = 1; i < length; i++) {
			for (int j = i; j > 0; j--) {
				if (arr[j - 1] < arr[j]) {
					tmp = arr[j - 1];
					arr[j - 1] = arr[j];
					arr[j] = tmp;
				}
			}
		}
	}
}
```