<!-- GFM-TOC -->
* [快速选择](#快速选择)
* [堆](#堆)
    * [215. Kth Element](#215-kth-element) medium c++ 20201223
* [桶排序](#桶排序)
    * [692. 出现频率最多的 k 个元素](#692-出现频率最多的-k-个元素) medium
    * [451. 按照字符出现次数对字符串排序](#451-按照字符出现次数对字符串排序)  medium
* [荷兰国旗问题](#荷兰国旗问题)
    * [75. 按颜色进行排序](#75-按颜色进行排序) medium
<!-- GFM-TOC -->


# 快速选择

用于求解   **Kth Element**   问题，也就是第 K 个元素的问题。

可以使用快速排序的 partition() 进行实现。需要先打乱数组，否则最坏情况下时间复杂度为 O(N<sup>2</sup>)。

# 堆

用于求解   **TopK Elements**   问题，也就是 K 个最小元素的问题。可以维护一个大小为 K 的最小堆，最小堆中的元素就是最小元素。最小堆需要使用大顶堆来实现，大顶堆表示堆顶元素是堆中最大元素。这是因为我们要得到 k 个最小的元素，因此当遍历到一个新的元素时，需要知道这个新元素是否比堆中最大的元素更小，更小的话就把堆中最大元素去除，并将新元素添加到堆中。所以我们需要很容易得到最大元素并移除最大元素，大顶堆就能很好满足这个要求。

堆也可以用于求解 Kth Element 问题，得到了大小为 k 的最小堆之后，因为使用了大顶堆来实现，因此堆顶元素就是第 k 大的元素。

快速选择也可以求解 TopK Elements 问题，因为找到 Kth Element 之后，再遍历一次数组，所有小于等于 Kth Element 的元素都是 TopK Elements。

可以看到，快速选择和堆排序都可以求解 Kth Element 和 TopK Elements 问题。

## 215. Kth Element

215\. Kth Largest Element in an Array (Medium)

[Leetcode](https://leetcode.com/problems/kth-largest-element-in-an-array/description/) / [力扣](https://leetcode-cn.com/problems/kth-largest-element-in-an-array/description/)

```text
Input: [3,2,1,5,6,4] and k = 2
Output: 5
```

题目描述：找到倒数第 k 个的元素。

**排序**  ：时间复杂度 O(NlogN)，空间复杂度 O(1)

```java
public int findKthLargest(int[] nums, int k) {
    Arrays.sort(nums);
    return nums[nums.length - k];
}
```

```c++
#include <iostream>
#include <vector>
#include <unordered_map>
using namespace std;
class Sort {
public:
    vector<int> execute(vector<int>& nums, int target) {
        sort(nums.begin(),nums.end());
        for(int e: nums)
            cout << e << " ";
        cout << endl;
    }
};

int main() {
    vector<int> nums = {0, 4, 3, 1, 7, 11, 15, 6};
    int target = 4;
    Sort().execute(nums, target);
    return 0;
}
```
**堆**  ：时间复杂度 O(NlogK)，空间复杂度 O(K)。

```java
public int findKthLargest(int[] nums, int k) {
    PriorityQueue<Integer> pq = new PriorityQueue<>(); // 小顶堆
    for (int val : nums) {
        pq.add(val);
        if (pq.size() > k)  // 维护堆的大小为 K
            pq.poll();
    }
    return pq.peek();
}
```
- c++ priority_queue介绍
定义：priority_queue<Type, Container, Functional>
Type 就是数据类型，Container 就是容器类型（Container必须是用数组实现的容器，比如vector,deque等等，但不能用 list。STL里面默认用的是vector），Functional 就是比较的方式，当需要用自定义的数据类型时才需要传入这三个参数，使用基本数据类型时，只需要传入数据类型，默认是大顶堆
一般是：

//升序队列  小顶堆  默认
priority_queue <int,vector<int>,greater<int> > q;
//降序队列  大顶堆
priority_queue <int,vector<int>,less<int> >q;

//greater和less是std实现的两个仿函数（就是使一个类的使用看上去像一个函数。其实现就是类中实现一个operator()
函数实现

方法：
```
和队列基本操作相同:

top 访问队头元素
empty 队列是否为空
size 返回队列内元素个数
push 插入元素到队尾 (并排序)
emplace 原地构造一个元素并插入队列
pop 弹出队头元素
swap 交换内容
```

```c++
int findKthLargest(vector<int>& nums, int k) {
    priority_queue<int, vector<int>, greater<int>> pq;//小顶堆 默认
    for(auto e: nums){
        pq.push(e);
        if(pq.size() > k) pq.pop();
    }
    return pq.top(); //不能使用pop()无返回值;
}
```

堆手写版
```c++

```

**快速选择**  ：时间复杂度 O(N)，空间复杂度 O(1)

```java
public int findKthLargest(int[] nums, int k) {
    k = nums.length - k;
    int l = 0, h = nums.length - 1;
    while (l < h) {
        int j = partition(nums, l, h);
        if (j == k) {
            break;
        } else if (j < k) {
            l = j + 1;
        } else {
            h = j - 1;
        }
    }
    return nums[k];
}

private int partition(int[] a, int l, int h) {
    int i = l, j = h + 1;
    while (true) {
        while (a[++i] < a[l] && i < h) ;
        while (a[--j] > a[l] && j > l) ;
        if (i >= j) {
            break;
        }
        swap(a, i, j);
    }
    swap(a, l, j);
    return j;
}

private void swap(int[] a, int i, int j) {
    int t = a[i];
    a[i] = a[j];
    a[j] = t;
}
```
```c++
int findKthLargest(vector<int>& nums, int k) {
    int lo = 0, hi = nums.size() - 1;
    sort(nums, lo, hi);//quicksort
    //for(auto e:nums)    cout << e <<" ";
    return nums[nums.size() - k];
}
int partition(vector<int>& nums, int lo, int hi){
    //swap 0作为守卫
    swap(nums, lo, hi);
    int i = lo, j = lo;
    for(;j < hi; j++){
        if(nums[j] < nums[hi]){
            //cout << "i:" << nums[i] << " j:" << nums[j] << " hi:" << nums[hi];
            swap(nums, i++, j);
        }
    }
    //swap
    swap(nums, i, j);
    return i;
}
void sort(vector<int>& nums, int lo, int hi){
    if(lo >= hi) return;
    int p = partition(nums, lo, hi);
    sort(nums, lo, p - 1);
    sort(nums, p + 1, hi);
}
void swap(vector<int>& nums, int i, int j){
    if(i == j) return;
    nums[i] = nums[i] ^ nums[j];
    nums[j] = nums[i] ^ nums[j];
    nums[i] = nums[i] ^ nums[j];
}
```
- 非递归优化版快排
```c++
int findKthLargest(vector<int>& nums, int k) {
    k = nums.size() - k;
    int lo = 0, hi = nums.size() - 1;
    while(lo <= hi){
        int i = lo, j = lo;
        swap(nums, lo, hi);
        for(;j < hi; j++){
            if(nums[j] <= nums[hi]){
                //cout << "i:" << nums[i] << " j:" << nums[j] << " hi:" << nums[hi];
                swap(nums, i++, j);
            }
        }
        //swap
        swap(nums, i, j);
        if(k == i) return nums[i];
        else if(k < i) hi = i-1;
        else lo = i+1;
    }
    return -1;
}
void swap(vector<int>& nums, int i, int j) {
    if (i != j) {
        nums[i] ^= nums[j];
        nums[j] ^= nums[i];
        nums[i] ^= nums[j];
    }
}
```
# 桶排序

## 692. 出现频率最多的 k 个元素

347\. Top K Frequent Elements (Medium)

[Leetcode](https://leetcode.com/problems/top-k-frequent-elements/description/) / [力扣](https://leetcode-cn.com/problems/top-k-frequent-elements/description/)

```html
Given [1,1,1,2,2,3] and k = 2, return [1,2].
```

设置若干个桶，每个桶存储出现频率相同的数。桶的下标表示数出现的频率，即第 i 个桶中存储的数出现的频率为 i。

把数都放到桶之后，从后向前遍历桶，最先得到的 k 个数就是出现频率最多的的 k 个数。

```java
public List<Integer> topKFrequent(int[] nums, int k) {
    Map<Integer, Integer> frequencyForNum = new HashMap<>();
    for (int num : nums) {
        frequencyForNum.put(num, frequencyForNum.getOrDefault(num, 0) + 1);
    }
    List<Integer>[] buckets = new ArrayList[nums.length + 1];
    for (int key : frequencyForNum.keySet()) {
        int frequency = frequencyForNum.get(key);
        if (buckets[frequency] == null) {
            buckets[frequency] = new ArrayList<>();
        }
        buckets[frequency].add(key);
    }
    List<Integer> topK = new ArrayList<>();
    for (int i = buckets.length - 1; i >= 0 && topK.size() < k; i--) {
        if (buckets[i] == null) {
            continue;
        }
        if (buckets[i].size() <= (k - topK.size())) {
            topK.addAll(buckets[i]);
        } else {
            topK.addAll(buckets[i].subList(0, k - topK.size()));
        }
    }
    return topK;
}
```

## 2. 按照字符出现次数对字符串排序

451\. Sort Characters By Frequency (Medium)

[Leetcode](https://leetcode.com/problems/sort-characters-by-frequency/description/) / [力扣](https://leetcode-cn.com/problems/sort-characters-by-frequency/description/)

```html
Input:
"tree"

Output:
"eert"

Explanation:
'e' appears twice while 'r' and 't' both appear once.
So 'e' must appear before both 'r' and 't'. Therefore "eetr" is also a valid answer.
```

```java
public String frequencySort(String s) {
    Map<Character, Integer> frequencyForNum = new HashMap<>();
    for (char c : s.toCharArray())
        frequencyForNum.put(c, frequencyForNum.getOrDefault(c, 0) + 1);

    List<Character>[] frequencyBucket = new ArrayList[s.length() + 1];
    for (char c : frequencyForNum.keySet()) {
        int f = frequencyForNum.get(c);
        if (frequencyBucket[f] == null) {
            frequencyBucket[f] = new ArrayList<>();
        }
        frequencyBucket[f].add(c);
    }
    StringBuilder str = new StringBuilder();
    for (int i = frequencyBucket.length - 1; i >= 0; i--) {
        if (frequencyBucket[i] == null) {
            continue;
        }
        for (char c : frequencyBucket[i]) {
            for (int j = 0; j < i; j++) {
                str.append(c);
            }
        }
    }
    return str.toString();
}
```

# 荷兰国旗问题

荷兰国旗包含三种颜色：红、白、蓝。

有三种颜色的球，算法的目标是将这三种球按颜色顺序正确地排列。它其实是三向切分快速排序的一种变种，在三向切分快速排序中，每次切分都将数组分成三个区间：小于切分元素、等于切分元素、大于切分元素，而该算法是将数组分成三个区间：等于红色、等于白色、等于蓝色。

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/7a3215ec-6fb7-4935-8b0d-cb408208f7cb.png"/> </div><br>


## 1. 按颜色进行排序

75\. Sort Colors (Medium)

[Leetcode](https://leetcode.com/problems/sort-colors/description/) / [力扣](https://leetcode-cn.com/problems/sort-colors/description/)

```html
Input: [2,0,2,1,1,0]
Output: [0,0,1,1,2,2]
```

题目描述：只有 0/1/2 三种颜色。

```java
public void sortColors(int[] nums) {
    int p0 = 0; //0的右界
    int p2 = nums.length-1; //2的左界
    int cur = 0;
    while(cur <= p2){
        if(nums[cur] == 0) swap(nums, cur++, p0++);
        else if(nums[cur] == 2) swap(nums, cur, p2--);//注意cur不能加
        else if(nums[cur] == 1) cur++;
    }
}
public void swap(int[] nums, int i, int j){
    if(i == j) return;
    nums[i] = nums[i] ^ nums[j];
    nums[j] = nums[i] ^ nums[j];
    nums[i] = nums[i] ^ nums[j];
}
```