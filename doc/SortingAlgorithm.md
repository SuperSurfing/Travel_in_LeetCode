### Absract

&emsp;&emsp;本文主要总结我对 [8 大排序算法](https://www.geeksforgeeks.org/bubble-sort/) 的总结，方便形象的理解和记忆，其中参考了 [Problem Solving with Algorithms and Data Structures using Python](http://interactivepython.org/runestone/static/pythonds/index.html) 和 [GeeksforGeeks](https://www.geeksforgeeks.org/fundamentals-of-algorithms/)。  

- [插入排序](#insection_sort)
- [冒泡排序](#bubble_sort)
- [归并排序](#merge_sort)
- [快速排序](#quick_sort)


### Insertion_Sort

参考《Introduction to Algorithms》 CH2，[Insertion sort](https://freefeast.info/general-it-articles/insertion-sort-pseudo-code-of-insertion-sort-insertion-sort-in-data-structure/) 最形象的比喻就是“抓牌”。  
1）首先将牌分为两组，左手是已排序的牌，右手从未排序的牌堆中抽取最上面的一张，  
2）再将其插入到左手的牌（序列）合适的位置中，使得左手牌序列依然有序。  
3）重复上面的操作，直到所有未排序的牌都抽完。  

![](https://freefeast.info/wp-content/uploads//2013/01/Insertion-Sort-Playing-Cards.jpeg)

> 1) Start with an empty left hand and cards face down on the table.
> 2) Then remove one card at a time from the table and Insert it into the correct position in the left hand.
> 3) To find a correct position for a card, we compare it with each of the cards already in the hand from right to left.

伪代码如下：

```
1.	    for j = 2 to n
2.	         key ← A [j]
3.         	// Insert A[j] into the sorted sequence A[1..j-1]
4.	         j ← i – 1
5.         while i > 0 and A[i] > key
6.                	A[i+1] ← A[i]
7.	                i ← i – 1
8.	        A[j+1] ← key
```



### Bubble_Sort

Bubble sort 又称为 Exchange sort ，参考《邓俊辉-数据结构》“Vector.BubbleSort”：  
1) 扫描未排序元素组，选出其中的最大者（最小者），将它放到队尾  
2) 在此扫描未排序元素组，选出次大者，置于倒数第二位  
3) 反复进行上述的扫描，直至未排序元素为 0
4) 最大者的选取方法犹如“接力比赛”，将“接力棒”从队首传到队尾，在传递的过程中，（相邻元素）谁的值大，谁拿“接力棒”往后走（交换位置）。  

伪代码（[wiki-bubble sort](https://en.wikipedia.org/wiki/Bubble_sort)）：

```
procedure bubbleSort( A : list of sortable items )
    n = length(A)
    repeat
        newn = 0
        for i = 1 to n-1 inclusive do
            if A[i-1] > A[i] then
                swap(A[i-1], A[i])
                newn = i
            end if
        end for
        n = newn
    until n <= 1
end procedure
```

《邓俊辉-数据结构》中的实现代码：
1) 尾部元素已有序，且为全局有序
2) 找最右侧的逆序对，分割有序和无序部分

```
template<typename T> void vector<T>::bubbleSort(Rank lo, Rank hi)
{
    while (lo < (hi = bubble(lo, hi)));
}

template<typename T> bool vector<T>::bubble(Rank lo, Rank hi)
{
    Rank last = lo;    // 最右侧的逆序对初始化为 [lo-1, lo]
    while(++lo < hi)   // 自左至右逐一检查各对相邻元素
        if (_elem[lo-1] > _elem[lo]) { // 如逆序，则
            last = lo; // 更新最右侧逆序对位置记录，并
            swap(_elem[lo-1] > _elem[lo]);  // 交换
        }
        
    return last;    // 返回最右侧逆序对的位置
}
```

### Merge_Sort

参考 [GeeksforGeeks - merge sort](https://www.geeksforgeeks.org/merge-sort/) :

```
MergeSort(arr[], l,  r)
If r > l
     1. Find the middle point to divide the array into two halves:  
             middle m = (l+r)/2
     2. Call mergeSort for first half:   
             Call mergeSort(arr, l, m)
     3. Call mergeSort for second half:
             Call mergeSort(arr, m+1, r)
     4. Merge the two halves sorted in step 2 and 3:
             Call merge(arr, l, m, r)
```

想象一下，每次从 A 和 B 两个数组取一个首部元素，比较之后再放入 C 数组，这就是合并的过程。   

参考《Introduction to Algorithms》CH3.1：  
Merge Sort 是典型的“the Divide and Conquer Algorithm”，它一般分为三步：分解、解决（子问题）、合并。它的递归式如下：

```math
T(n) = \left\{\begin{matrix}
\Theta(1) & n \leq c\\ 
 aT(n/b) + D(n) + C(n)& other
\end{matrix}\right.
```


### Quick_Sort

参考 [GeeksforGeeks - quick sort](https://www.geeksforgeeks.org/quick-sort/) 和《邓俊辉-数据结构》CH12 QuickSort，同 merge sort 一样，quick sort 也是“a Divide and Conquer Algorithm”。其中，Merge sort 的计算量和难点在“**合**”，而 Quick sort 在于“**分**”：  

1) 求 pivot（轴点），分割，再递归（尾递归）
2) 设置low 和 high 两个指针（two pointers），一趟循环，交替前进

![](https://note.youdao.com/yws/public/resource/d968916d4caea412213b0fc124cfdebc/xmlnote/4D20EC35CC02485D9ADB7AC8F8DD17DE/11503)

伪代码如下：

```
/* low  --> Starting index,  high  --> Ending index */
quickSort(arr[], low, high)
{
    if (low < high)
    {
        /* pi is partitioning index, arr[pi] is now
           at right place */
        pi = partition(arr, low, high);

        quickSort(arr, low, pi - 1);  // Before pi
        quickSort(arr, pi + 1, high); // After pi
    }
}
```

LGU （Less - Unsorted - Greater）版实现 partition() :

```
template<typename T> Rank vector<T>::partition(Rank lo, Rank hi) { // [lo, hi)
    swap(_elem[lo], _elem[lo + rand() % (hi - lo)]);
    hi--;
    T pivot = _elem[lo];    // 经过以上随机交互，等于随机选取轴点
    while (lo < hi) { // two pointer，从两端向中间交替前进
        while (lo < hi && pivot <= _elem[hi])
            hi--;    // 向左拓展 G
        _elem[lo] = _elem[hi];    // 凡小于轴点者，皆归入 L
        while (lo < hi && _elem[lo] <= pivot)
            lo++;    // 向右拓展 L
        _elem[hi] = _elem[lo];    // 凡大于轴点者，皆归入 G
    } // assert lo == hi
    _elem[lo] = pivot;    // 轴点归位
    return lo;
}
```

![](https://note.youdao.com/yws/public/resource/d968916d4caea412213b0fc124cfdebc/xmlnote/4FC3F3845C574FC79CB3BB5A6596B803/11552)