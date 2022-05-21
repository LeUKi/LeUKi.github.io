---
title: 最大连续子序列小结
tags:
  - 动态规划
categories:
  - 算法
comments: true
date: 2022-05-21 23:51:26
---
# 题目

输出其的和与首尾元素。
原题：HDOJ 1231

# 题解

动态规划:

- `dp` ：以 `a[i]` 结尾的最大连续子列和，`a[i]` 是当前遍历元素
- 状态转移方程： `dp[i]=max(dp[i-1]+a[i],a[i])`
- 状态初始化：`dp[0]=a[0]`

一些细节：

- 定义变量`start`、`end`为子序列的首尾索引值，即最大和是`dp[end]`
- 当 `dp[i-1]+a[i] > a[i]` 且 `dp[i] > dp[end]`，意味着最大子序列由此开始，即`start`、`end`都置当前位`i`
- 当 `dp[i-1]+a[i] < a[i]` 时，意味着当前位纳入最大子序列范围，即`end`置当前位`i`

```c++
#include <iostream>
#include <vector>
using namespace std;

int main()
{   int k,j;
    vector <int> v;
    vector <int> dp;
    while(1){
        v.clear();
        dp.clear();
        cin>>k;
        if (k==0)return 0;
        for (int i = 0; i < k; ++i) {
            v.push_back((cin>>j,j));
        }

        int t,start=0,end=0,max=v[0],oldlast;
        dp.push_back(v[0]);
        for (int i=1;i<v.size();i++) {
            oldlast=dp.back();
            t=oldlast+v[i];
            if (v[i]>t){
                dp.push_back(v[i]);
                if (v[i]>dp[end]){
                    start=i;
                    end=i;
                }
            }else{
                dp.push_back(t);
                if (t>dp[end])end=i;
            }
        }
        if (dp[end]>0)cout<<dp[end]<<" "<<v[start]<<" "<<v[end]<<endl;
        else cout<<0<<" "<<v[0]<<" "<<v.back()<<endl;
    }
}
```

