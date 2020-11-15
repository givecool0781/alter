---
tags: Leetcode
---
# Big Sorting
## 題目
給你一個陣列，其中有包含很大的數字
要你排列
ex:

$$
 \left[
 \begin{matrix}
   100 & 8 & 110 & 13548789794564131\\
  \end{matrix}
  \right] \
$$
要排序成
$$
 \left[
 \begin{matrix}
   8 & 100 & 110 & 13548789794564131\\
  \end{matrix}
  \right] \
$$

## Solve
### 最初想法
利用sorted函式來做排序，但後來發現題目的陣列是使用string去儲存的
使用sorted可能會發生:
$$
 \left[
 \begin{matrix}
   1 & 10 & 3 & 313548789794564131 & 3 & 5\\
  \end{matrix}
  \right] \
$$
排序結果
$$
 \left[
 \begin{matrix}
   1 & 10 & 3 & 3 & 313548789794564131 & 5\\
  \end{matrix}
  \right] \
$$
會是string的排序方式
```python=1
# Complete the bigSorting function below.
def bigSorting(unsorted):
    return  sorted(unsorted)
```
### 改良
使用將string轉換為int來排序
```python=1
# Complete the bigSorting function below.
def bigSorting(unsorted):
    return  sorted(unsorted , key=int)
```
但是會遇到時間timeout的問題
### 不只要對 還要很快
後來查到可以使用lamdba來解決問題
#### lamdba(工具人函數)
隨用隨丟 真是方便
```python=
lambda 參數1, 參數2, …: 運算式A if 關係運算式 else 運算式B
```
簡單來說就是你想幹啥就幹啥
只是運算式A必須只有一行

#### Sorted
python 的sorted函數是包含兩種排序演算法
> Timsort 融合合併排序 (Merge Sort) 和插入排序 (Insertion Sort) 兩種排序演算法。個數少用就是插入排序，個數多則用合併排序。差別是這個合併排序有點不一樣，裡面引用了一個簡單的概念增加排序的效果，其概念是「在現實情況中，大部分的序列裡面會藏有部分早就排序好的小片段，由於這些小片段不需要再花時間排序，所以抓出這些小片段就可以減少排序的時間

透過預設的陣列我發現python的sorted只透過len(x)跟x去判斷會有誤差的問題
那就兩個一起判斷
$key = lambda x : (len(x) , x)$
```python=1
def bigSorting(unsorted):
    s = sorted(unsorted , key = lambda x : (len(x),x))
    return  s
```
就成功了
這只是簡單的題目欸 怎麼這麼難