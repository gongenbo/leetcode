## 排序
```c++
string s="ngram";
sort(s.begin(), s.end());
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