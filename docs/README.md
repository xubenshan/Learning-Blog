# **前言**

> 整理的学习笔记

笔记站点是由`docsify`搭建成的，具体的搭建过程可以移步到[docsify搭建教程](/docsify/docsify.md)。另外可以参考[官方文档](https://docsify.js.org/#/)。

# **数据结构与算法**

## c语言

## c++语言

<!-- tabs:start -->

#### **C++**

```cpp
#include <iostream>
using namespace std;

const int N = 10;
int f[N][N];
int ans;
int n;
void dfs(int index, int y, int sum)
{
    if (index == n)
    {
        ans = max(ans, sum);
        return;
    }
    dfs(index + 1, y, sum + f[index + 1][y]);
    dfs(index + 1, y + 1, sum + f[index + 1][y + 1]);

}

int main()
{  
    cin >> n;
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j <= i; j++)//数塔只需要输入j <= i的部分
        {
            cin >> f[i][j];
        }
    }
    dfs(0, 0, f[0][0]);//这句代码意思是已经选择完第0层，选的是(0,0)，当前的sum是f[0][0]。
    // dfs(0, 0, 0);error
    cout << ans<< endl;
    return 0;
}
```


#### **java**

Bonjour!

#### **python**

Ciao!

<!-- tabs:end -->
```cpp
#include <iostream>
using namespace std;
```