## 一、深度优先搜索(DFS)+回溯

`DFS`是一种搜索的策略，简单来说就是一条路走到黑。当走到尽头之后就回退到上一个结点，继续一条路走到黑。回退的过程就叫做**回溯**。
`DFS`一般采用**递归**的方式实现。<!--more-->

> 对递归的详细讲解会在以后出一个独立的专题，小伙伴们可以期待一下噢！
>
> `DFS`可以用一个递归搜索树来形象描述，那这棵树长什么样子呢，小伙伴们继续往下看。
> ![在这里插入图片描述](https://img-blog.csdnimg.cn/b46f5fe9bde34fbd907b714c6ea1284c.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5omT6JOd5qGl5p2v55qE6YCa5L-h5Lq6,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)
> 事实上对所有的合法`DFS`求解过程都可以把它画成树的形式，死胡同就相当于叶子结点。分岔口就相当于非叶子结点。
> 对某个DFS类型的题目，不妨把一些状态作为树的结点，问题就变得很直观了。
>
> `DFS`搜索的顺序是A-B-D-E-C-F。从结点A出发，它有两条路可以走，我们选择最左边那一条，到达结点B，结点B有两个分支，选择最左边那个，到达结点D。结点D没有路可走了也就是到达死胡同了，返回上一个结点B，也就是回溯的过程。B还有一条路可走，到达结点E。同理结点E回溯到结点B，结点B没有分支了，回溯到上一个结点A，结点A还有一个分支可以走，到达结点C,结点C有一个分支到达结点F，结点F是死胡同。至此所有的结点都访问了，搜索结束。
> 其实DFS的搜索顺序和树的先序遍历是一样的。树的先序遍历就是根左右。

从递归树我们就能看出`DFS`的时间复杂度是很高的，是$O(2^n)$。所以我们常说暴力搜索嘛，就是因为它时间复杂度太高了，当数据很大时很容易就`TLE(`超时)的。同时我们还能看出`DFS`会走遍所有的路径，并且走到死胡同就代表一条完整的路径形成。因此==深度优先搜索是一种枚举所有路径，遍历所有情况的搜索策略==。

***

## 二、DFS模板

> 在备战蓝桥杯的过程中记住一些算法模板还是非常重要滴。

```cpp
#include <iostream>
using namespace std;
bool check()
{
	...
}
void dfs()
{
	if (满足边界条件)
	{
		
		return;
	}
	for (int i = 0; i < 可扩展的路径数; i++)
	{
		if (check())
		{
			修改现场;
			dfs(下一种情况);
			还原现场;
		}
	}
}	
```

> 模板不是固定不变的，我们要根据题目灵活地运用它。

***

## 三、DFS经典例题

### 1.模板题——迷宫问题

[题目链接](https://www.luogu.com.cn/problem/P1605)
![在这里插入图片描述](https://img-blog.csdnimg.cn/76bfafbf85ae400bbf980124689c8b74.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5omT6JOd5qGl5p2v55qE6YCa5L-h5Lq6,size_20,color_FFFFFF,t_70,g_se,x_16)
**题目分析**

> 迷宫问题是拿来练习DFS与BFS很经典的题目。迷宫问题有很多种问法，比如迷宫从起点到终点有没有路径，有几条，最短路径是多少。

求从起点到终点的方案数显而易见也是要用`DFS`，遍历所有的情况。我们要考虑这样一个问题，迷宫里的某点`(x,y)`是否要被访问呢。当这点是障碍物肯定不能访问，该点不在迷宫里面也不能访问，该点访问过了那就不能访问了。(题目中有每个方格最多经过一次)。因此我们需要一个`check()`函数来判断某一点是否合法。合法我们就去访问该点。

> 其实这个过程就是一个剪枝的过程，根据题目条件限制，剪掉一些不可能存在解的分支。

另外我们该如何知道某点是障碍点呢，可以设置一个map数组来表示该迷宫。

* 当`map[x][y]==1`时表示该点是障碍点 
 * `map[x][y]==0`表示该点是正常点

**AC代码**

```cpp
#include <iostream>
using namespace std;

const int N = 100;

int dx[4] = {0, 0, -1, 1};
int dy[4] = {1, -1, 0, 0};//方向数组技巧
int n, m, T;//n行m列T障碍总数
int ans;//记录方案总数
int sx, sy, fx, fy, l, r;//起点坐标(sx,sy)终点坐标(fx,fy)障碍点坐标(l,r)
bool visited[N][N];//记录某点是否被访问过
int map[N][N];//map[i][j] == 1表示是障碍

bool check(int x, int y)//check某点是否合法
{
    if (x < 1 || x > n || y < 1 || y > m) return false;//该点出界不合法
    if (map[x][y]) return false;//该点是障碍点不合法
    if (visited[x][y]) return false;//该点被访问过不合法
    return true;//其他情况访问合法
}

void dfs(int x, int y)//dfs维护点的坐标参数
{
    if (x == fx && y == fy)//满足边界条件，到达终点
    {
        ans++;//方案数+1
        return;
    }
    for (int i = 0; i < 4; i++)//枚举四个方向
    {
        int newx = x + dx[i];
        int newy = y + dy[i];
        if (check(newx, newy))//该点合法
        {
            visited[x][y] = true;//将(x,y)设置成已访问,修改现场
            dfs(newx, newy);//dfs下一个点
            visited[x][y] = false;//回溯,恢复现场
        }
    }
}

int main()
{
    cin >> n >> m >> T;
    cin >> sx >> sy >> fx >> fy;
    while(T--)
    {
        cin >> l >> r;
        map[l][r] = 1;
    }
    dfs(sx, sy);//从起点开始搜索
    cout << ans << endl;
    return 0;
}
```

> 小伙伴们每道例题都要好好看一下AC代码噢，上面有很详细的注释。

> 这道题还可以优化下空间，可以只用maze数组来表示迷宫，同时记录迷宫内的某点是否访问过。具体见下面的代码。

```cpp
//空间优化
#include <iostream>
using namespace std;

const int N = 100;

int dx[4] = {0, 0, -1, 1};
int dy[4] = {1, -1, 0, 0};//方向数组
int n, m, T;
int ans;
int sx, sy, fx, fy, l, r;
//bool visited[N][N];
int map[N][N];//map[i][j] == 1表示是障碍
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          
bool check(int x, int y)//判断某点是否可以访问
{
    if (x < 1 || x > n || y < 1 || y > n) return false;
    if (map[x][y] || map[x][y] == 3 ) return false;//该点是障碍点或已经访问过，不能访问
    //if (visited[x][y]) return false;
    return true;
}

void dfs(int x, int y)
{
    if (x == fx && y == fy)
    {
        ans++;
        return;
    }
    for (int i = 0; i < 4; i++)
    {
        int newx = x + dx[i];
        int newy = y + dy[i];
        if (check(newx, newy))
        {
            map[x][y] = 3;//标记成已访问
            dfs(newx, newy);
            //点(x,y)能访问说明它不是障碍点所以回溯要让map[x][y]=0
            //而不是map[x][y]=1
            map[x][y] = 0;
        }
    }
}
int main()
{
    cin >> n >> m >> T;
    cin >> sx >> sy >> fx >> fy;
    while(T--)
    {
        cin >> l >> r;
        map[l][r] = 1;
    }
    dfs(sx, sy);
    cout << ans << endl;
    return 0;
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/f0d98badf856489392bc3a7bfad24d98.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5omT6JOd5qGl5p2v55qE6YCa5L-h5Lq6,size_20,color_FFFFFF,t_70,g_se,x_16)

### 2.01背包问题(DFS暴力搜索)

[题目链接](https://www.acwing.com/problem/content/2/)
![背包问题](https://img-blog.csdnimg.cn/597a9a9e51c24576a62a7ad2d74e9b21.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5omT6JOd5qGl5p2v55qE6YCa5L-h5Lq6,size_20,color_FFFFFF,t_70,g_se,x_16)
**题目分析**

> 01背包问题是一个很经典的问题，它有多种解法。DFS是其中一种，在学习动态规划的时候还会提到它噢。
>
> 第i件物品无非就是选和不选两种情况，在搜索的过程中DFS函数必须要记录当前处理的物品编号`index`，当前背包的容量`sumW`，当前的总价值`sumC`。

* 当不选第`index`个物品时，那么`sumW`,`sumC`是不变的，接着处理第`index+1`个物品，也就是`DFS(index+1, sumW, sumC)`。
* 当选择第`index`个物品时，`sumW`变成`sumW+w[index]`，`sumC`变成`sumC+v[index]`，接着处理第`index+1`个物品，也就是`DFS(index+1, sumW+w[index],sumC+v[index])`。边界条件也就是把最后一件物品也处理完了，即`index=n`（注意默认index从0开始）。

当一条分支结束了该干什么呢，很简单呀就是判断该分支最终满不满足总重量不大于背包容量。即`sumW<=v`。满足的话我们就更新价值`maxvalue`，即`maxvalue=max(maxvalue,sumC)`。

**AC代码**

```cpp
//01背包问题的dfs版本
#include <iostream>
#include <algorithm>

using namespace std;

const int N = 10010;
int n, v, maxvalue;
int w[N], c[N];
//DFS维护三个参数，正在选第index个物品，当前的总体积，当前的总价值
void dfs(int index, int sumW, int sumC)
{
    if (index == n)
    {
        if (sumW <= v)
        {
            maxvalue = max(maxvalue, sumC);
        }
        return;
    }
    dfs(index + 1, sumW, sumC);//不选第index个物品
    dfs(index + 1, sumW + w[index], sumC + c[index]);//选第index个物品
}

int main()
{
    cin >> n >> v;
    for (int i = 0; i < n; i++)
    {
        cin >> w[i] >> c[i];
    }
    dfs(0, 0, 0);//开始时对第1件物品进行选择，此时背包重量0价值也是0
    cout << maxvalue << endl;
    return 0;
}
```

> 当然了01背包问题如果用`DFS`来解决的话，当数据比较大时，是不能`AC`的。这道题会超出时间限制。即便经过剪枝也是无能为力的。

![在这里插入图片描述](https://img-blog.csdnimg.cn/b9204460d99f411dae0c590f14f4196a.png)


### 3.回溯——[USACO1.5]八皇后 Checker Challenge

[题目链接](https://www.luogu.com.cn/problem/P1219)
![在这里插入图片描述](https://img-blog.csdnimg.cn/e0392de0426f4359962c51f77cf5484f.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5omT6JOd5qGl5p2v55qE6YCa5L-h5Lq6,size_20,color_FFFFFF,t_70,g_se,x_16)
![在这里插入图片描述](https://img-blog.csdnimg.cn/d9ae3a9ad53f44418de0d2a2f06c8c4b.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5omT6JOd5qGl5p2v55qE6YCa5L-h5Lq6,size_20,color_FFFFFF,t_70,g_se,x_16)
**题目分析**

>八皇后问题是学习回溯很经典的例题，这道题是八皇后问题的扩展，N皇后问题。也就是棋盘的大小是任意的。

这道题`DFS`的思路还是比较清晰的，每行有且只有一个棋子，那么`DFS`可以记录下当前处理的是第几行的棋子。假设当前处理的是第`i`行的棋子，那么要枚举处在该行的棋子位置，判断哪个是合法的。
什么样的位置算是合法的呢，这个位置的列还有左对角线，右对角线位置都不能有棋子。那么又该如何表示这些位置呢？我们采用一维数组来分别表示列，左对角线，右对角线。列很好表示就是`b[j]`，左对角线我们可以发现行减去列的绝对值是恒定的，即`c[i-j+n]`,右对角线行加列是恒定的。即`d[i+j]`。

>小伙伴们可以自己画画图看一看噢~
>
>当某位置放置了棋子，那么就将和它同列同对角线的位置都取为1，即`b[j]=1`,`c[i-j+n]=1`,`d[i+j]=1`。

**AC代码**

```cpp
#include <iostream>
using namespace std;

int a[100], b[100], c[100], d[100];//a[]储存解b列c左斜d右斜
int n;//棋盘大小
int ans;

bool check(int i, int j)//检查(i,j)是否合法
{
    if (!b[j] && !c[j - i + n] && !d[j + i]) return true;//b[j],c[i-j+n],d[i+j]为0说明该点可以放置棋子。
    return false;
}

void dfs(int i)//dfs第i行棋子
{   //边界条件
    if (i > n)//dfs完所有的棋子
    {
     	ans++;
        if (ans <= 3)//只要前三个解
        {
            for (int i = 1; i <= n; i++)//输出解
            {
                cout << a[i] << ' ';
                
            }
            cout << endl;  
        }
        return;     
    }
    
        for (int j = 1; j <= n; j++)//枚举一行的所有位置
        {	//(i,j)点满足放棋子的条件，我们就把棋子放在(i,j)点
            if (check(i, j))
            {
                a[i] = j;//把满足解的列号存在a[i]中
                b[j] = 1;//修改现场
                c[ j - i + n] = 1;
                d[j + i] = 1;
                dfs(i + 1);//处理下一行的棋子
                b[j] = 0;//回溯，恢复现场
                c[j - i + n] = 0;
                d[j + i] = 0;
            }
        }
}
int main()
{
    cin >> n;
    dfs(1);
    cout << ans << endl;
    return 0;
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/c37e19018b064ee88491028af5bec829.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5omT6JOd5qGl5p2v55qE6YCa5L-h5Lq6,size_20,color_FFFFFF,t_70,g_se,x_16)

### 4.递归实现排列型枚举

[题目链接](https://www.acwing.com/problem/content/96/)
![在这里插入图片描述](https://img-blog.csdnimg.cn/93f1e3da7444452c827100778284df39.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5omT6JOd5qGl5p2v55qE6YCa5L-h5Lq6,size_20,color_FFFFFF,t_70,g_se,x_16)
**题目分析**

>DFS可以用来处理排列组合问题。
>
>对于全排列问题我们可以这样想，第1个位置可以放`1~n`任意一个数，第2个位置可以放除了放在第1个位置的数以外的任何一个数，以此类推。因此我们可以画出一个递归搜索树，用`map[]`来表示储存当前排列。`DFS`函数要记住当前处理的是第`index`个位置，从1到n进行遍历，看看这个数是否可以放在第`index`个位置，需要有一个判重数组`hashtable[x]`来记录`x`是否在排列里面。

**AC代码**

```cpp
#include <iostream>
using namespace std;

const int N = 11;
//map[N]储存当前的排列，hashtable[N]判断某个数是否在排列里
int map[N];
bool hashtable[N];面。
int n;

void dfs(int index)//当前填第index位置
{
    if (index == n + 1)//已经处理完1~n个位置
    {
        for (int i = 1; i <= n; i++)//输出当前排列
        {
            cout << map[i] << ' ';
        }
        cout << endl;
        return;
    }
    for (int i = 1; i <= n; i++)//枚举1~n
    {
        if (hashtable[i] == false)//当i这个数没有填在map中
        {
            map[index] = i;//第index位置填入i这个数
            hashtable[i] = true;//记i在当前排列
            dfs(index + 1);//处理第index+1位置
            //处理完map[index]=i的子问题，恢复现场
            hashtable[i] = false;
            map[index] = 0;
        }
    }
}
int main()
{
    cin >> n;
    dfs(1);//从1这个数开始搜索
    return 0;
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/de6462dec44d47daa0afa1023d8a0c89.png)

### 5.递归实现组合型枚举

[题目链接](https://www.acwing.com/problem/content/95/)
![在这里插入图片描述](https://img-blog.csdnimg.cn/e84e6dee11d64d5688a7e07c419aa54b.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5omT6JOd5qGl5p2v55qE6YCa5L-h5Lq6,size_20,color_FFFFFF,t_70,g_se,x_16)
![在这里插入图片描述](https://img-blog.csdnimg.cn/36278db485514eff94f4487f54653173.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5omT6JOd5qGl5p2v55qE6YCa5L-h5Lq6,size_20,color_FFFFFF,t_70,g_se,x_16)
**题目分析**
组合和排列的最大区别就是组合不需要考虑顺序，也就是说`123`和`132`是一样的。
由于题目要求同一行的数必须按升序排序，因此可以让`DFS`函数记录当前处理的第`index`个位置，可以选的最小数`start`。

>虽然参数变成了两个，但是不需要判重数组了。

`DFS`的思路是这个样子的，假设当前处理的是第`index`个位置，这个位置可以放置`start~n`其中任意一个数。接着处理第`index+1`个位置，这个位置可以放置的最小数是前一位数的下一个数。即`i+1~n`。


**AC代码**

```cpp
#include <iostream>
using namespace std;

const int N = 30;

int map[N];//存储解
int n, m;
//dfs记录当前处理的第index个位置，可以选的最小数start
void dfs(int index, int start)
{
    if (index > m)//m个位置都处理完了
    {
        for (int i = 1; i <= m; i++)//输出方案
        {
            cout << map[i] << " ";
        }
        cout << endl;
        return;
    }
    //第index个位置可以选择start~n里面的数
    for (int i = start; i <= n; i++)
    {
        map[index] = i;
        //处理index+1位置，能选择的最小数是前面选择的数+1
        dfs(index + 1, i + 1);
        //处理完第index位置放置i这个数的子问题后回溯。
        map[index] = 0;
      
    }
}

int main()
{
    cin >> n >> m;
    dfs(1, 1);
    return 0;
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/353f2858c0d24affbfb1c9307427a79c.png)

***

## 四、剪枝思想

前面也提到过剪枝的概念，现在详细说下剪枝这种东西。我们知道`DFS`时间复杂度是很高的，如果不进行一些优化的话，在数据很大的情况下很容易就爆`TLE`。这个时候我们就可以用剪枝这种东西来优化啦~
在进行`DFS`的过程中对某条可以确定不存在解的分支采用直接剪短的策略。这样会大大降低计算量。一个搜索树剪掉一些分支就形象的叫它剪枝了。
==剪枝一般都是利用题目的限制条件来确定哪些分支是不可能存在解的。==

***

## 五、剪枝思想在DFS中的应用

小伙伴们来回忆下01背包问题，我们是在选择完所有物品后才进行判断，看看背包总体积是否超过背包容量。是不是可以在选择的过程中就加入这一判断，这样就可以减少很多的计算量。当选第`index`件物品时，如果选上它那么背包的总体积就超出背包容量，我们一定不能选了。此时选第`index`件物品的分支就不可能存在解，直接剪掉。

```cpp
//DFS维护三个参数，正在选第index个物品，当前的总体积，当前的总价值
void dfs(int index, int sumW, int sumC)
{
    if (index == n)//选择完所有的物品，最终的sumW一定不大于v
    {
        maxvalue = max(maxvalue, sumC);
        return;
    }
    dfs(index + 1, sumW, sumC);//不选第index个物品
    if (sum + w[index] <= v)//剪枝
    {   //选第index个物品
    	dfs(index + 1, sumW + w[index], sumC + c[index]);
    } 
}
```

小伙伴们再来回忆下前面的组合型枚举问题，我们也可以用到剪枝来优化。可以看出要是剩下的数全都用上也满足不了一共m个数的要求，那么我们直接可以结束这个分支了。即`n - start + index < m`。

```cpp
void dfs(int index, int start)
{
	if (n - start + index < m) return;//剪枝
    if (index > m)//m个位置都处理完了
    {
        for (int i = 1; i <= m; i++)//输出方案
        {
            cout << map[i] << " ";
        }
        cout << endl;
        return;
    }
    //第index个位置可以选择start~n里面的数
    for (int i = start; i <= n; i++)
    {
        map[index] = i;
        //处理index+1位置，能选择的最小数是前面选择的数+1
        dfs(index + 1, i + 1);
        //处理完第index位置放置i这个数的子问题后回溯。
        map[index] = 0;
      
    }
}

```

> 通过下表我们能看出剪枝之后的运行速度确实快了不少。
> ![在这里插入图片描述](https://img-blog.csdnimg.cn/3f184725aed44b37bdb9b40924995a4b.png)

***

# 写在后面

>想到啥就说啥了，给备战蓝桥杯的小伙伴们提些建议。

我不推荐大家去`leetcode`上刷题，因为`leetcode`的形式和蓝桥杯是不太一样的。力扣只需要写函数，输入输出已经内置好了。蓝桥杯的输入输出是需要自己写的。另外呢力扣主要是面向找工作的，题目是面试用的，不是专门打比赛的。因此题目不太适合蓝桥杯竞赛。当然了里面的题目还是很经典的，专门学某一算法是可以刷力扣的。我给大家推荐几个适合的网站还有书籍。

[ACwing网站](https://www.acwing.com/)
[洛谷](https://www.luogu.com.cn/)
[C语言网蓝桥杯题库](https://www.dotcpp.com/oj/train/)
[蓝桥杯练习系统](http://lx.lanqiao.cn/problemsets.page)
[蓝桥杯官网题库](https://www.lanqiao.cn/problems/?sort=students_count&category_id=3)
![在这里插入图片描述](https://img-blog.csdnimg.cn/da7e876c11b741df8c7d3d5b71ab38f8.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5omT6JOd5qGl5p2v55qE6YCa5L-h5Lq6,size_12,color_FFFFFF,t_70,g_se,x_16)
![在这里插入图片描述](https://img-blog.csdnimg.cn/b811a601fe264db3988a7eca92347a1f.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5omT6JOd5qGl5p2v55qE6YCa5L-h5Lq6,size_20,color_FFFFFF,t_70,g_se,x_16)
![在这里插入图片描述](https://img-blog.csdnimg.cn/df58c6e5577e47d5a9fd70ca73d21e06.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5omT6JOd5qGl5p2v55qE6YCa5L-h5Lq6,size_11,color_FFFFFF,t_70,g_se,x_16)

![在这里插入图片描述](https://img-blog.csdnimg.cn/a799d7696df843f3b8a57695348148cc.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5omT6JOd5qGl5p2v55qE6YCa5L-h5Lq6,size_11,color_FFFFFF,t_70,g_se,x_16)

> 这几个网站和书是我一直在用的，真心推荐给大家~

美好的时光总是短暂的，又到了说再见的时候啦~一键三连支持一下吧！
![在这里插入图片描述](https://img-blog.csdnimg.cn/174d4b7d8830426085d94f82fa74bd55.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5omT6JOd5qGl5p2v55qE6YCa5L-h5Lq6,size_15,color_FFFFFF,t_70,g_se,x_16#pic_center)