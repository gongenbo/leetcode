## 排序
### sort
```c++
string s="ngram";
sort(s.begin(), s.end());
```
### 优先队列 priority_queue
它的模板声明带有三个参数，priority_queue<Type, Container, Functional>
Type 为数据类型， Container 为保存数据的容器，Functional 为元素比较方式。
Container 必须是用数组实现的容器，比如 vector, deque 但不能用 list.
STL里面默认用的是 vector. 比较方式默认用 operator< , 所以如果你把后面俩个
参数缺省的话，优先队列就是大顶堆，队头元素最大。
#### 1. 默认大顶堆
```c++
priority_queue<int> q;
for( int i= 0; i< 10; ++i ) q.push(i);
while( !q.empty() ){
    cout<<q.top()<<endl;
    q.pop();
}
```
### 2. 小顶堆
```c++
priority_queue<int, vector<int>, greater<int> > q;
for( int i= 0; i< 10; ++i ) q.push(10-i);
while( !q.empty() ){
    cout << q.top() << endl;
    q.pop();
}
```
## 数组
新建数组,26个字母每个初始化为0
```c++
vector<int> table(26, 0);
```
## 字符串
### 1. 交换
```c++
swap(s[left], s[right])
```
### 2.转数组
```c++
for
```
### 3.查找位置
```
s.find(s[i])
```
## 集合
```c++
int longestPalindrome(string s) {
    unordered_map<char, int> count;
    int ans = 0;
    for (char c : s)
        ++count[c];
    for (auto p : count) {
        int v = p.second;
        ans += v / 2 * 2;
        if (v % 2 == 1 and ans % 2 == 0)
            ++ans;
    }
    return ans;
}
```
### 长度
```c++
map.size();
```
### 查找位置
是否存在
如果key存在，则find返回key对应的迭代器，如果key不存在，则find返回unordered_map::end。因此可以通过
```c++
map.find(key) == map.end()
```
```c++
unordered_map<int,int>::iterator iter = record.find(target - nums[i]);
if(iter != record.end() && iter->second != i)
    return {i, iter->second};
```