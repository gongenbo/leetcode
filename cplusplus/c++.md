## 排序
### sort
```c++
string s="ngram";
sort(s.begin(), s.end());
```
```
451
class Solution {
public:
    string frequencySort(string s) {
        unordered_map<char,int> mem;
        for(auto c:s) mem[c]++;
        sort(s.begin(),s.end(),[&mem](char a,char b){
            if(mem[a]==mem[b]) return a>b;
            return mem[a]>mem[b];});
        return s;
    }
};
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
### 1. 初始化
新建数组,26个字母每个初始化为0
```c++
vector<int> table(26, 0);
```
### 2. vector.emplace_back()与push_back()区别
emplace_back是c++11之后的，效率更高。

```
struct S{
    int value;
};

std::vector<S> v;
v.push_back({0}); //没问题
v.emplace_back({0}); //编不过
```
emplace_back是模板函数，对于{0}它无法确定是啥东东。push_back不是模板函数，它会直接构造一个对应的对象拷过去。
### 3. pop_back()
弹出

## 字符串
### 引入
using namespace std;//导入后才能使用string
### 1. 长度
str.size()
### 2. 交换
```c++
swap(s[left], s[right])
```
### 3.转数组
```c++
for
```
### 3.查找位置
```
s.find(s[i])
```

## 集合
### 引入
```
#include<set>
```
### 初始化
```
set<char> vowel{'a','e','i','o','u'};
```
### 是否包含count
1 包含，0不包含
