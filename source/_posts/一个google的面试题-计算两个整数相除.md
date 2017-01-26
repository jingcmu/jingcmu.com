title: 一个google的面试题 计算两个整数相除
date: 2014-09-17 20:07:09
categories: 编程
tags: [算法, Google]
---
Divide number and return result in form of a string. e.g 100/3 result should be 33.(3) Here 3 is in brackets because it gets repeated continuously and 5/10 should be 0.5.

这题难在怎么去判断循环和记录循环出现的位置

上代码：

```
#include "common.hpp"  
  
string caldec(int a, int b) {  
    string s = "";  
    int residule = a%b;   
    unordered_map<int, int> residule_index; //记录出现过的残差的值和位置  
    s += to_string(a/b);  
    s += ".";  
    int index = s.length();  
    while(residule != 0 && residule_index.find(residule) == residule_index.end()) {  
        residule_index[residule] = index++;  
        s += to_string((residule*10)/b);  
        residule = (residule*10)%b;  
    }  
    if(residule_index.find(residule) != residule_index.end()) {  
        int i = residule_index[residule];  
        s.insert(i, "(");  
        s += ")";  
    }  
    if(s[s.length()-1] == '.') {  
        s = s.substr(0, s.length() - 1);  
    }  
    return s;  
}  
//我最近比较喜欢用随机数进行测试  
int main() {  
    srand(time(NULL));  
    for(int i=0; i<10; i++) {  
        int a = rand()%101;  
        int b = rand()%29;  
        if(a > b && b != 0) {  
            cout << "a = " << a << ", b = " << b << ", res = " << caldec(a, b) << endl;  
        }  
    }  
    return 0;  
}  
```