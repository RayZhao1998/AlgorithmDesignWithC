# 算法设计技巧与分析 c语言实现
## 第一章 算法分析基本概念
### 1.1 LINEARSEARCH 线性查找
输入： 数组a, 数组a的长度 len，要查找的元素 x。

输出：如果查找到，返回下标；否则输出-1.

```c
int linearSearch(int a[], int len, int x) {
	int j = 0;
	while (j < len && x != a[j]) {
		j++;
	}
	if (x == a[j]) {
		return j;
	} else {
		return -1;
	}
}
```

### 1.2 BINARYSEARCH 二分查找
输入：升序数组a, 数组a的长度 len， 要查找的元素 x。

输出：如果查找到，返回下标；否则输出-1.

```c
int binarySearch(int a[], int len, int x) {
	int low = 0;
	int high = len - 1;
	int mid;
	int j = -1;
	while(low <= high && j == -1) {
		mid = (low + high) / 2;
		if (x == a[mid]) {
			j = mid;
		} else if (x < a[mid]) {
			high = mid - 1;
		} else {
			low = mid + 1;
		}
	}
	return j;
}
```

### 1.3 MERGE 合并
输入：数组a，数组a的长度 len，三个索引p, q, r, 0<=p<=q<=r<=len-1, 子数组a[p...q]和a[q+1...r]各自按升序排列。

输出：合并两个子数组后的数组a[p...r]。

```c
void merge(int a[], int len, int p, int q, int r) {
	int s = p;
	int t = q + 1;
	int k = p;
	// 辅助数组b
	int *b = (int*)malloc(sizeof(int) * （r-p+1);
	while(s <= q && t <= r) {
		if (a[s] <= a[t]) {
			b[k] = a[s];
			s++;
		} else {
			b[k] = a[t];
			t++;
		}
		k++;
	}
	if (s == q + 1) {
		for (int i=t;i<=r;i++) {
			b[i-t+k] = a[i];
		} 
	} else {
		for (int i=s;i<=q;i++) {
			b[i-s+k] = a[i];
		}
	}
	for (int i=p;i<=r;i++) {
		a[i] = b[i];
	}
}

```

### 1.4 SELECTIONSORT 选择排序

输入： 数组a，数组a的长度 len。

输出：按非降序排列的数组

```c
void selectionSort(int a[], int len) {
	int k;
	for (int i=0;i<len-1;i++) {
		k = i;
		for (int j=i+1;j<len;j++) {
			if (a[j] < a[k]) {
				k = j;
			}
		}
		if (k != i) {
			int temp = a[i];
			a[i] = a[k];
			a[k] = temp;
		}
	}
}
```

### 1.5 INSERTIONSORT 插入排序

输入：带排序数组a，数组a的长度 len。

输出：按非降序排列的数组

```c
void insertionSort(int a[], int len) {
	int x;
	int j;
	for (int i=1;i<len;i++) {
		x = a[i];
		j = i-1;
		while(j >= 0 && a[j] > x) {
			a[j+1] = a[j];
			j--;
		}
		a[j+1] = x;
	}
}

```

### 1.6 BOTTOMUPSORT 自底向上合并排序

输入：带排序数组a，数组a的长度 len。

输出：按非降序排列的数组

```c
void buttomUpSort(int a[], int len) {
	int t = 1;
	int s, i;
	while(t <= len) {
		s = t;
		t = 2 * s;
		i = 0;
		while(i+t <= len) {
			merge(a, len, i, i+s-1, i+t-1);
			i += t;
		}
		if (i+s < len) {
			merge(a, len, i, i+s-1, len-1);
		}
	}
}
```

> 感觉算法上没有什么问题，但是运行时会出现指针错误的问题，尚未找到问题的关键。待纠正。

### 1.7 BRUTE-FORCE PRIMALITYTEST 素数测试蛮力算法
输入：正整数n>=2.

输出：如果n是素数输出真，否则为假。

```c
bool primalityTest(int n) {
	int s = sqrt(n);
	for (int i=2;i<=s;i++) {
		if (n % i == 0) return false;
	}
	return true;
}
```

### 1.11 PSUM

输入：n = k^2，k为某刻整数

输出：1到n之间每个完全平方数j, 1+2+...+j的值

```c
void psum(int n) {
	int k = sqrt(n);
	int *sum = (int*)malloc(sizeof(int) * (k+1));
	for (int i=1;i<=k;i++) {
		sum[i] = 0;
		for (int j=1;j<=i*i;j++) {
			sum[i] += j;
		}
	}
	for (int i=1;i<=k;i++) {
		cout<<sum[i]<<" ";
	}
}
```

### 1.16 BUBBLESORT 冒泡排序

输入：带排序数组a，数组a的长度 len。

输出：按非降序排列的数组

```c
void bubbleSort(int a[], int len) {
	int i = 0;
	bool sorted = false;
	while(i < len-1 && !sorted) {
		sorted = true;
		for (int j=len-1;j>=i+1;j--) {
			if (a[j] < a[j-1]) {
				int temp = a[j];
				a[j] = a[j-1];
				a[j-1] = temp;
				sorted = false;
			}
		}
		i++;
	}
}
```

### 1.17 EUCLID 最大公约数

输入：两个正整数a,b。

输出：a，b的最大公约数。
```c
int euclid(int a, int b) {
	int r = 1;
	while(r != 0) {
		r = a % b;
		a = b;
		b = r;
	}
	return a;
}
```