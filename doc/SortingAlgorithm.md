### Absract

&emsp;&emsp;������Ҫ�ܽ��Ҷ� [8 �������㷨](https://www.geeksforgeeks.org/bubble-sort/) ���ܽᣬ������������ͼ��䣬���вο��� [Problem Solving with Algorithms and Data Structures using Python](http://interactivepython.org/runestone/static/pythonds/index.html) �� [GeeksforGeeks](https://www.geeksforgeeks.org/fundamentals-of-algorithms/)��  

- [��������](#insection_sort)
- [ð������](#bubble_sort)
- [�鲢����](#merge_sort)
- [��������](#quick_sort)


### Insertion_Sort

�ο���Introduction to Algorithms�� CH2��[Insertion sort](https://freefeast.info/general-it-articles/insertion-sort-pseudo-code-of-insertion-sort-insertion-sort-in-data-structure/) ������ı������ǡ�ץ�ơ���  
1�����Ƚ��Ʒ�Ϊ���飬��������������ƣ����ִ�δ������ƶ��г�ȡ�������һ�ţ�  
2���ٽ�����뵽���ֵ��ƣ����У����ʵ�λ���У�ʹ��������������Ȼ����  
3���ظ�����Ĳ�����ֱ������δ������ƶ����ꡣ  

![](https://freefeast.info/wp-content/uploads//2013/01/Insertion-Sort-Playing-Cards.jpeg)

> 1) Start with an empty left hand and cards face down on the table.
> 2) Then remove one card at a time from the table and Insert it into the correct position in the left hand.
> 3) To find a correct position for a card, we compare it with each of the cards already in the hand from right to left.

α�������£�

```
1.	    for j = 2 to n
2.	         key �� A [j]
3.         	// Insert A[j] into the sorted sequence A[1..j-1]
4.	         j �� i �C 1
5.         while i > 0 and A[i] > key
6.                	A[i+1] �� A[i]
7.	                i �� i �C 1
8.	        A[j+1] �� key
```



### Bubble_Sort

Bubble sort �ֳ�Ϊ Exchange sort ���ο����˿���-���ݽṹ����Vector.BubbleSort����  
1) ɨ��δ����Ԫ���飬ѡ�����е�����ߣ���С�ߣ��������ŵ���β  
2) �ڴ�ɨ��δ����Ԫ���飬ѡ���δ��ߣ����ڵ����ڶ�λ  
3) ��������������ɨ�裬ֱ��δ����Ԫ��Ϊ 0
4) ����ߵ�ѡȡ�������硰�������������������������Ӷ��״�����β���ڴ��ݵĹ����У�������Ԫ�أ�˭��ֵ��˭�á��������������ߣ�����λ�ã���  

α���루[wiki-bubble sort](https://en.wikipedia.org/wiki/Bubble_sort)����

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

���˿���-���ݽṹ���е�ʵ�ִ��룺
1) β��Ԫ����������Ϊȫ������
2) �����Ҳ������ԣ��ָ���������򲿷�

```
template<typename T> void vector<T>::bubbleSort(Rank lo, Rank hi)
{
    while (lo < (hi = bubble(lo, hi)));
}

template<typename T> bool vector<T>::bubble(Rank lo, Rank hi)
{
    Rank last = lo;    // ���Ҳ������Գ�ʼ��Ϊ [lo-1, lo]
    while(++lo < hi)   // ����������һ����������Ԫ��
        if (_elem[lo-1] > _elem[lo]) { // ��������
            last = lo; // �������Ҳ������λ�ü�¼����
            swap(_elem[lo-1] > _elem[lo]);  // ����
        }
        
    return last;    // �������Ҳ�����Ե�λ��
}
```

### Merge_Sort

�ο� [GeeksforGeeks - merge sort](https://www.geeksforgeeks.org/merge-sort/) :

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

����һ�£�ÿ�δ� A �� B ��������ȡһ���ײ�Ԫ�أ��Ƚ�֮���ٷ��� C ���飬����Ǻϲ��Ĺ��̡�   

�ο���Introduction to Algorithms��CH3.1��  
Merge Sort �ǵ��͵ġ�the Divide and Conquer Algorithm������һ���Ϊ�������ֽ⡢����������⣩���ϲ������ĵݹ�ʽ���£�

```math
T(n) = \left\{\begin{matrix}
\Theta(1) & n \leq c\\ 
 aT(n/b) + D(n) + C(n)& other
\end{matrix}\right.
```


### Quick_Sort

�ο� [GeeksforGeeks - quick sort](https://www.geeksforgeeks.org/quick-sort/) �͡��˿���-���ݽṹ��CH12 QuickSort��ͬ merge sort һ����quick sort Ҳ�ǡ�a Divide and Conquer Algorithm�������У�Merge sort �ļ��������ѵ��ڡ�**��**������ Quick sort ���ڡ�**��**����  

1) �� pivot����㣩���ָ�ٵݹ飨β�ݹ飩
2) ����low �� high ����ָ�루two pointers����һ��ѭ��������ǰ��

![](https://note.youdao.com/yws/public/resource/d968916d4caea412213b0fc124cfdebc/xmlnote/4D20EC35CC02485D9ADB7AC8F8DD17DE/11503)

α�������£�

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

LGU ��Less - Unsorted - Greater����ʵ�� partition() :

```
template<typename T> Rank vector<T>::partition(Rank lo, Rank hi) { // [lo, hi)
    swap(_elem[lo], _elem[lo + rand() % (hi - lo)]);
    hi--;
    T pivot = _elem[lo];    // ������������������������ѡȡ���
    while (lo < hi) { // two pointer�����������м佻��ǰ��
        while (lo < hi && pivot <= _elem[hi])
            hi--;    // ������չ G
        _elem[lo] = _elem[hi];    // ��С������ߣ��Թ��� L
        while (lo < hi && _elem[lo] <= pivot)
            lo++;    // ������չ L
        _elem[hi] = _elem[lo];    // ����������ߣ��Թ��� G
    } // assert lo == hi
    _elem[lo] = pivot;    // ����λ
    return lo;
}
```

![](https://note.youdao.com/yws/public/resource/d968916d4caea412213b0fc124cfdebc/xmlnote/4FC3F3845C574FC79CB3BB5A6596B803/11552)