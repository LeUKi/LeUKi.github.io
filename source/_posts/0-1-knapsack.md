---
title: 01背包问题小结
tags:
  - 01背包
categories:
  - 算法
comments: true
date: 2022-04-21 10:47:53
---
先上代码
```c++
#include <iostream>
#include <algorithm>
using namespace std;
int main() {
    int M,N;
    cin>>M>>N;
    int W[N],C[N];+_
    int dp[N][M+1];
    //接收
    for (int i = 0; i < N; ++i) {
        cin>>W[i]>>C[i];
    }
    //初始化
    for (int i = 0; i < N; ++i) {
        dp[i][0]=0;
    }
    for (int i = 1; i < M+1; ++i) {
        if (W[0]<=i)dp[0][i]=C[0];
        else dp[0][i]=0;
    }
    //dp
    for (int i = 1; i < N; ++i) {
        for (int j = 0; j < M+1 ;++j) {
            if (j<W[i]) { dp[i][j] = dp[i - 1][j]; }
            else { dp[i][j] = max(dp[i - 1][j], dp[i - 1][j - W[i]] + C[i]);
            }
        }
    }
//    for (int i = 0; i < N; ++i) {
//        for (int j = 0; j < M+1 ;++j) {
//            cout<<dp[i][j]<<" ";
//        }
//        cout<<endl;
//    }

    cout<<dp[N-1][M];
    return 0;
}
```

`dp[i][j]` 表示从下标为 `0` ~ `i` 的物品里任意取，放进容量为 `j` 的背包，价值总和最大是多少。

每次放进一个物品，每次增加一个背包容量，当物品放不进背包（`j<W[i]`）时，取放进物品前的最好值（即`dp[i-1][j]`）。即在图中取上一格的值；

```c++
if (j<W[i]) { dp[i][j] = dp[i - 1][j]; }
```

当物品可以放进背包时，考虑放与不放。

- 不放：价值取图中上一格的值（即`dp[i-1][j]`）。
- 放：价值取下面两者的和：
  - 该物品的价值（即`C[i]`）。
  - 先放进该物品后剩余的背包空间（`[j - W[i]`）与 不放该物品情况（`[i - 1]`） 下的值（`dp[i - 1][j - W[i]`）。后者是先前计算好的最优值，所以整体肯定是最优解。

```c++
dp[i][j] = 
    max(
        dp[i - 1][j], //不放
        dp[i - 1][j - W[i]] + C[i] //放
	);
```