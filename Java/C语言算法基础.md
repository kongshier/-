# 算法基础

## 递归和递推

### 递归

```
递归算法在计算机系统中用栈帮助实现，一般常见的算法有深度优先遍历（DFS），可以解决的问题有迷宫问题是否连通的问题，递推会对应一个递归搜索树，递归搜索树可以帮助我们更好的理解递归的流程，递归要注意的有是否可以进行剪枝，在迷宫问题中，也要考虑是否要保存原有的迷宫。
```

#### 入门例题

##### 递归实现指数型枚举

```
从 1∼n 这 n 个整数中随机选取任意多个，输出所有可能的选择方案。

输入格式
输入一个整数 n。

输出格式
每行输出一种方案。

同一行内的数必须升序排列，相邻两个数用恰好 1 个空格隔开。

对于没有选任何数的方案，输出空行。

本题有自定义校验器（SPJ），各行（不同方案）之间的顺序任意。

数据范围
1≤n≤15
输入样例：
3
输出样例：

3
2
2 3
1
1 3
1 2
1 2 3
```

题解：

对于指数型枚举一个数只有选与不选的区分，所以我们从第一个位置，枚举到第n个位置，在第i个位置上，i这个数只有选与不选的区别，选的话我们将st[i]记录为i；不选记录为-1；一直到u>n时枚举了所有的位置，此时输出即可，要注意的是在输出完后要记得return掉

```c++
#include<cstdio>
#include<cstring>
#include<iostream>
#include<algorithm>

using namespace std;

const int N=20;
int n;
int st[N];
void dfs(int u){
    if(u>n){
        for(int i=1;i<=n;i++){
            if(st[i]==1) cout<<i<<" ";
        }
        cout<<endl;
        return ;
    }
    
    st[u]=1;
    dfs(u+1);
    
    st[u]=-1;
    dfs(u+1);
}
int main(){
    cin>>n;
    dfs(1);
    return 0;
}
```

##### 递归实现排列型枚举

```
把 1∼n 这 n 个整数排成一行后随机打乱顺序，输出所有可能的次序。

输入格式
一个整数 n。

输出格式
按照从小到大的顺序输出所有方案，每行 1 个。

首先，同一行相邻两个数用一个空格隔开。

其次，对于两个不同的行，对应下标的数一一比较，字典序较小的排在前面。

数据范围
1≤n≤9
输入样例：
3
输出样例：
1 2 3
1 3 2
2 1 3
2 3 1
3 1 2
3 2 1
```

题解

在排列型枚举中，我们有n个位置，在每个位置上分别枚举这个位置可以放那个数，所以我们有一个path数组来记录排列的方案，使用st的bool数组来判断这个数是否选过。

```c++
#include<cstdio>
#include<cstring>
#include<iostream>
#include<algorithm>

using namespace std;

const int N=15;
int n;
bool st[N];
int path[N];
void dfs(int u){
    if(u>n){//所有位置枚举完成
        for(int i=1;i<=n;i++){
            cout<<path[i]<<" ";
        }
        cout<<endl;
        return ;
    }
    
    for(int i=1;i<=n;i++){//在第u个位置上枚举所有方案，这个位置上可以放置所有没有被用过的数字。
        if(!st[i]){
            path[u]=i;
            st[i]=true;//表示这个数被用过了
            dfs(u+1);
            st[i]=false;//还原状态，保证回溯时下一层递归一致。
        }
    }
}
int main(){
    cin>>n;
    dfs(1);
    
    return 0;
}
```

##### 递归实现组合型枚举

```
从 1∼n 这 n 个整数中随机选出 m 个，输出所有可能的选择方案。

输入格式
两个整数 n,m ,在同一行用空格隔开。

输出格式
按照从小到大的顺序输出所有方案，每行 1 个。

首先，同一行内的数升序排列，相邻两个数用一个空格隔开。

其次，对于两个不同的行，对应下标的数一一比较，字典序较小的排在前面（例如 1 3 5 7 排在 1 3 6 8 前面）。

数据范围
n>0 ,
0≤m≤n ,
n+(n−m)≤25
输入样例：
5 3
输出样例：
1 2 3 
1 2 4 
1 2 5 
1 3 4 
1 3 5 
1 4 5 
2 3 4 
2 3 5 
2 4 5 
3 4 5 
```

题解

在组合数枚举中，我们可以通过认为确定枚举的顺序来通过类似排列数的方法来实现，不同的一点时在排列数枚举时，我们要在传一个参数num表示前一位枚举到那个数字，首先写一个朴素方法，该方法的时间是1601ms

```c++
#include<cstdio>
#include<cstring>
#include<iostream>
#include<algorithm>

using namespace std;

const int N=25;
int n,m;
int path[N];
bool st[N];
void dfs(int u,int num){
    if(u>m){
        for(int i=1;i<=m;i++){
            cout<<path[i]<<" ";
        }
        cout<<endl;
        return;
    }
    
    
    for(int i=1;i<=n;i++){
        if(!st[i]&&i>num){
            st[i]=true;
            path[u]=i;
            dfs(u+1,i);
            st[i]=false;
        }
    }
}
int main(){
    cin>>n>>m;
    dfs(1,0);
    
    return 0;
}
```

下面做一个优化

我们在递归前提前判断一个，上一个位置的数是否合理，如果后面剩的数字不能满足m个位置和递增的条件就直接return掉，进行剪枝，优化时间复杂度。该方法的时间是103ms

```
#include<cstdio>
#include<cstring>
#include<iostream>
#include<algorithm>

using namespace std;

const int N=25;
int n,m;
int path[N];
bool st[N];
void dfs(int u,int num){
    if(num>n-m+u-1)return;
    if(u>m){
        for(int i=1;i<=m;i++){
            cout<<path[i]<<" ";
        }
        cout<<endl;
        return;
    }
    
    
    for(int i=1;i<=n;i++){
        if(!st[i]&&i>num){
            st[i]=true;
            path[u]=i;
            dfs(u+1,i);
            st[i]=false;
        }
    }
}
int main(){
    cin>>n>>m;
    dfs(1,0);
    
    return 0;
}
```

#### 迷宫问题

通过深度优先搜索（DFS）方法实现。

##### 迷宫问题一

```
一天蒜头君掉进了一个迷宫里面，蒜头君想逃出去，可怜的蒜头君连迷宫是否有能逃出去的路都不知道。

看在蒜头君这么可怜的份上，就请聪明的你告诉蒜头君是否有可以逃出去的路。

输入格式
第一行输入两个整数 nn 和 mm，表示这是一个 n \times mn×m 的迷宫。

接下来的输入一个 nn 行 mm 列的迷宫。其中 'S' 表示蒜头君的位置，'*'表示墙，蒜头君无法通过，'.'表示路，蒜头君可以通过'.'移动，'T'表示迷宫的出口（蒜头君每次只能移动到四个与他相邻的位置——上，下，左，右）。

输出格式
输出一个字符串，如果蒜头君可以逃出迷宫输出"yes"，否则输出"no"。

数据范围
1 \le n, m \le 101≤n,m≤10。

输出时每行末尾的多余空格，不影响答案正确性

样例输入1复制
3 4
S**.
..*.
***T
样例输出1复制
no
样例输入2复制
3 4
S**.
....
***T
样例输出2复制
yes
```

题解

我们读入所有数据，然后获得起点S的坐标。然后深度优先遍历，在迷宫问题中进入DFS后，要先判断是否到中点，在判断是否是障碍物，然后标记该点访问过了。

```
#include<cstdio>
#include<cstring>
#include<iostream>
#include<algorithm>

using namespace std;
const int N=15;
int n,m;
char g[N][N];
int dx[4]={-1,0,1,0},dy[4]={0,1,0,-1};
bool st[N][N];
bool dfs(int x,int y){
    if(g[x][y]=='T'){
        return true;
    }
    if(g[x][y]=='*') return false;
    st[x][y]=true;
    for(int i=0;i<4;i++){
        int a=x+dx[i],b=y+dy[i];
        if(a>n||a<=0||b<=0||b>m)continue;
        if(st[a][b])continue;
        if(dfs(a,b)){
            return true;
        }
    }
    return false;
}
int main(){
    cin>>n>>m;
    int x,y;
    for(int i=1;i<=n;i++){
        for(int j=1;j<=m;j++){
            cin>>g[i][j];
            if(g[i][j]=='S'){
                x=i;
                y=j;
            }
        }
    }
    if(dfs(x,y)){
        cout<<"yes"<<endl;
    }else{
        cout<<"no"<<endl;
    }
    
    return 0;
}
```

##### 迷宫问题二

```xml
蒜头君在你的帮助下终于逃出了迷宫，但是蒜头君并没有沉浸于喜悦之中，而是很快的又陷入了思考，从这个迷宫逃出的最少步数是多少呢？

输入格式
第一行输入两个整数 nn 和 mm，表示这是一个 n \times mn×m 的迷宫。

接下来的输入一个 nn 行 mm 列的迷宫。其中 'S' 表示蒜头君的位置，'*'表示墙，蒜头君无法通过，'.'表示路，蒜头君可以通过'.'移动，'T'表示迷宫的出口（蒜头君每次只能移动到四个与他相邻的位置——上，下，左，右）。

输出格式
输出整数，表示蒜头君逃出迷宫的最少步数，如果蒜头君无法逃出迷宫输出 -1−1。

数据范围
1 \le n, m \le 101≤n,m≤10。

输出时每行末尾的多余空格，不影响答案正确性

样例输入1复制
3 4
S**.
..*.
***T
样例输出1复制
-1
样例输入2复制
3 4
S**.
....
***T
样例输出2复制
5
```

题解

本题要求判断是否可以到达并且要计算出最短路径，其实用宽度优先搜索更为合适，因为宽度优先搜索第一次到达目的地就是最短路径，但是我们使用深度优先也可以实现，我们定义一个最短量来储存最短的路径，当每一次到达目的点就比较一下与最短路的大小，交换最短路径长度，因此我们要遍历所有的可行路径，所以就要回溯访问状态，所以在一个遍历后就要复原，将一个点置为未访问，额额额，在 这道题中，我开始忘了读入n和m所以出现了segment段错误，还检查了好久没查到。

```c++
#include<cstdio>
#include<cstring>
#include<iostream>
#include<algorithm>

using namespace std;
const int N=15;
char g[N][N];
bool st[N][N];
int Min=99999;
int m,n;
int dx[4]={-1,0,1,0},dy[4]={0,1,0,-1};
void dfs(int x,int y,int stmp){
    if(stmp>Min) return ;
    if(g[x][y]=='T'){
        Min=min(Min,stmp);
        return;
    }  
    st[x][y]=true;
    if(g[x][y]=='*') return ;
    for(int i=0;i<4;i++){
        int a=x+dx[i],b=y+dy[i];
        if(a>n||a<=0||b>m||b<=0) continue;
        if(st[a][b]) continue;
        if(g[a][b]=='*') continue;
        dfs(a,b,stmp+1);
        st[a][b]=false;
        
    }
}
int main(){
    cin>>n>>m;
    int a,b;
    for(int i=1;i<=n;i++){
        for(int j=1;j<=m;j++){
            cin>>g[i][j];
            if(g[i][j]=='S'){
                a=i,b=j;
            }
        }
    }
    dfs(a,b,0);
    if(Min==99999){
        cout<<-1<<endl;
    }else{
        cout<<Min<<endl;
    }
    return 0;
}
```

##### 迷宫问题三

```
经过思考蒜头君终于解决了怎么计算一个迷宫的最短路问题，于是蒜头君找到一个新的迷宫图，来验证自己是否真的会计算一个迷宫的最短路。

为了检验自己计算的是否正确，蒜头君特邀你一起来计算。

输入格式
第一行输入两个整数 nn 和 mm，表示这是一个 n \times mn×m 的迷宫。

接下来的输入一个 nn 行 mm 列的迷宫。其中'@'表示蒜头君的位置，'#'表示墙，蒜头君无法通过，'.'表示路，蒜头君可以通过'.'移动，所有在迷宫最外围的'.'都表示迷宫的出口（蒜头君每次只能移动到四个与他相邻的位置——上，下，左，右）。

输出格式
输出整数，表示蒜头君逃出迷宫的最少步数，如果蒜头君无法逃出迷宫输出 -1−1。

数据范围
1 \le n,m \le 151≤n,m≤15。

输出时每行末尾的多余空格，不影响答案正确性

样例输入1复制
9 13
#############
#@..........#
#####.#.#.#.#
#...........#
#.#.#.#.#.#.#
#.#.......#.#
#.#.#.#.#.#.#
#...........#
#####.#######
样例输出1复制
11
样例输入2复制
4 6
#.####
#.#.##
#...@#
######
样例输出2复制
5

```

题解

该迷宫问题与第二个迷宫问题类似，我们也要求出最短路径，所以一样要使用minn记录短的路径。

但是这个题要注意到达的条件，和第二个迷宫终点判断不一样，这个题要观察迷宫的构造，判断终止条件。所以这道题尽量从1开始存储迷宫图。

```c++
#include<cstdio>
#include<cstring>
#include<iostream>
#include<algorithm>

using namespace std;
const int N=20;
int n,m;
int dx[4]={-1,0,1,0},dy[4]={0,1,0,-1};
char g[N][N];
bool st[N][N];
int minn=99999;
void dfs(int x,int y,int stmp){
    if(stmp>minn)return ;
    if(x==0||y==0||x==n+1||y==m+1){
        minn=min(minn,stmp);
        return ;
    }
    st[x][y]=true;
    for(int i=0;i<4;i++){
        int a=x+dx[i],b=y+dy[i];
        if(g[a][b]=='#')continue;
        if(st[a][b])continue;
        dfs(a,b,stmp+1);
        st[a][b]=false;
    }

}
int main(){
    cin>>n>>m;
    int x,y;
    for(int i=1;i<=n;i++){
        for(int j=1;j<=m;j++){
            cin>>g[i][j];
            if(g[i][j]=='@'){
                x=i;y=j;
            }
        }
    }
    dfs(x,y,0);
    if(minn==99999){
        cout<<-1<<endl;
    }else{
        cout<<minn-1<<endl;
    }
    return 0;
}
```

好了，dfs递归就先写到这里，之后图论的时候我们在聊。

### 递推

#### 入门例题

##### 斐波那契数列

```
输入一个整数 n ，求斐波那契数列的第 n 项。

假定从 0 开始，第 0 项为 0。

数据范围
0≤n≤39
样例
输入整数 n=5 

返回 5
```

题解

该题十分基础，我们要理解斐波那契数列的组成，数列中从每一项都是前两项的和，所以如果不要求存下一些数的数值，我们就可以直接使用，几个变量操作不用进行数组创建。

```c++
class Solution {
public:
    int Fibonacci(int n) {
        if(n<=1)return n;
        if(n==2) return 1;
        int a=1,b=1;
        int t;
        for(int i=3;i<=n;i++){
            t=a+b;
            a=b;
            b=t;
        }
        return t;
    }
};
```

##### 费解的开关

```
你玩过“拉灯”游戏吗？

25 盏灯排成一个 5×5 的方形。

每一个灯都有一个开关，游戏者可以改变它的状态。

每一步，游戏者可以改变某一个灯的状态。

游戏者改变一个灯的状态会产生连锁反应：和这个灯上下左右相邻的灯也要相应地改变其状态。

我们用数字 1 表示一盏开着的灯，用数字 0 表示关着的灯。

下面这种状态

10111
01101
10111
10000
11011
在改变了最左上角的灯的状态后将变成：

01111
11101
10111
10000
11011
再改变它正中间的灯后状态将变成：

01111
11001
11001
10100
11011
给定一些游戏的初始状态，编写程序判断游戏者是否可能在 6 步以内使所有的灯都变亮。

输入格式
第一行输入正整数 n，代表数据中共有 n 个待解决的游戏初始状态。

以下若干行数据分为 n 组，每组数据有 5 行，每行 5 个字符。

每组数据描述了一个游戏的初始状态。

各组数据间用一个空行分隔。

输出格式
一共输出 n 行数据，每行有一个小于等于 6 的整数，它表示对于输入数据中对应的游戏状态最少需要几步才能使所有灯变亮。

对于某一个游戏初始状态，若 6 步以内无法使所有灯变亮，则输出 −1。

数据范围
0<n≤500
输入样例：
3
00111
01011
10001
11010
11100

11101
11101
11110
11111
11111

01111
11111
11111
11111
11111
输出样例：

3
2
-1
```

题解

该题我们分析可以发现，我们可以通过枚举第一行的5个灯的32中开与不开的状态来实现，因为第一行开关确定以后，第一行的开关亮与不亮只与下一层开关有关，如果i-1行j列是关的，我们就开一下i行j列的灯就可以使上一个灯泡开，一次递推我们就可以实现是否所有灯都能开，要注意的是我们要保存一下开始的灯泡状态，因为要枚举32次，积累一下位运算>>

我们可以通过op>>i&1表示第一行的灯是否开，这是通过二进制存储实现的，我们用0表示不开，用1表示开。

```c++
#include<cstdio>
#include<cstring>
#include<iostream>
#include<algorithm>

using namespace std;
const int N=510;
char g[6][6],backup[6][6];
int dx[6]={-1,0,1,0,0},dy[6]={0,1,0,-1,0};
int n;
void turn(int x,int y){
    for(int i=0;i<5;i++){
        int a=x+dx[i],b=y+dy[i];
        if(a<0||a>=5||b<0||b>=5)continue;
        g[a][b]^=1;
    }
}
int main(){
    cin>>n;
    while(n--){
        for(int i=0;i<5;i++)cin>>g[i];
        
        int ans=10;
        for(int op=0;op<32;op++){
            memcpy(backup,g,sizeof g);
            int stmp=0;
            for(int i=0;i<5;i++){
                if(op>>i&1){
                    turn(0,i);
                    stmp++;
                }
            }
            
            
            for(int i=1;i<5;i++){
                for(int j=0;j<5;j++){
                    if(g[i-1][j]=='0'){
                        turn(i,j);
                        stmp++;
                    }
                }
            }
            
            bool suf=true;
            for(int j=0;j<5;j++){
                if(g[4][j]=='0'){
                    suf=false;
                    break;
                }
            }
            
            if(suf){
                ans=min(ans,stmp);
            }
            
            memcpy(g,backup,sizeof backup);
        }
        if(ans>6){
            cout<<-1<<endl;
        }else{
            cout<<ans<<endl;
        }
    }
    
    return 0;
}
```

## 二分和前缀和

### 二分

#### 二分简介

```markdown
二分分为整数二分和实数二分两种，
#### 整数二分步骤：

1. 找一个区间[L, R]，使得答案一定在该区间中
2. 找一个判断条件，使得该判断条件具有二段性，并且答案一定是该二段性的分界点。
3. 分析中点M在该判断条件下是否成立，如果
   （成立，考虑答案在那个区间。如果不成立，考虑答案在那个区间）
4. 如果更新方式写的是R = Mid，则此时l=mid+1，这是mid更新方式是
   如果更新方式是l=mid;则mid=l+r+1>>1;c此时r=mid-1；
```

#### 入门例题

##### 二分查找一

```xml
蒜头君手上有个长度为 nn 的数组 AA。由于数组实在太大了，所以蒜头君也不知道数组里面有什么数字，所以蒜头君会经常询问整数 xx 是否在数组 AA 中。

输入格式
第一行输入两个整数 nn 和 mm，分别表示数组的长度和查询的次数。

接下来一行有 nn 个整数 a_ia 
i
​
 。

接下来 mm 行，每行有 11 个整数 xx，表示蒜头君询问的整数。

输出格式
对于每次查询，如果可以找到，输出"YES"，否则输出"NO"。

数据范围
1≤n,m≤1e5 0≤x≤1e6

输出时每行末尾的多余空格，不影响答案正确性

样例输入复制
10 5
1 1 1 2 3 5 5 7 8 9
0
1
4
9
10
样例输出复制
NO
YES
NO
YES
NO
```

```c++
#include<cstdio>
#include<cstring>
#include<iostream>
#include<algorithm>

using namespace std;
const int N=1e5+10;
int num[N];
int n,m;

int main(){
    cin>>n>>m;
    for(int i=0;i<n;i++)cin>>num[i];
    sort(num,num+n);
    while(m--){
        int t;
        cin>>t;
        int l=0,r=n-1;
        while(l<r){
            int mid=l+r>>1;    
            if(num[mid]>=t){
                r=mid;
            }else{
                l=mid+1;
            }
        }
        if(num[l]!=t){
            cout<<"NO"<<endl;
        }else{
            cout<<"YES"<<endl;
        }
    }
    
    
    return 0;
}
```

##### 二分查找二

```
蒜头君手上有个长度为 nn 的数组 AA。由于数组实在太大了，所以蒜头君也不知道数组里面有什么数字，所以蒜头君会经常询问在数组 AA 中，大于等于 xx 的最小值是多大？

输入格式
第一行输入两个整数 nn 和 mm，分别表示数组的长度和查询的次数。

接下来一行有 nn 个整数 a_ia 
i
​
 。

接下来 mm 行，每行有 11 个整数 xx，表示蒜头君询问的整数。

输出格式
对于每次查询，如果可以找到，输出这个整数。

否则输出 -1。

数据范围
1≤n,m≤1e5 0≤x≤1e6

输出时每行末尾的多余空格，不影响答案正确性

样例输入复制
10 5
1 1 1 2 3 5 5 7 8 9
0
1
4
9
10
样例输出复制
1
1
5
9
-1
```

题解

```c++
#include<cstdio>
#include<cstring>
#include<iostream>
#include<algorithm>

using namespace std;
const int N=1e6+10;
int n,m;
int num[N];
int main(){
    cin>>n>>m;
    for(int i=0;i<n;i++)cin>>num[i];
    sort(num,num+n);
    while(m--){
        int t;
        cin>>t;
        int l=0,r=n-1;
        while(l<r){
            int mid=l+r>>1;
            if(num[mid]>=t){
                r=mid;
            }else{
                l=mid+1;
            }
        }
        if(num[l]>=t){
            cout<<num[l]<<endl;
        }else{
            cout<<-1<<endl;
        }
    }
    
    return 0;
}
```



##### 二分查找三

```
蒜头君手上有个长度为 nn 的数组 AA。由于数组实在太大了，所以蒜头君也不知道数组里面有什么数字，所以蒜头君会经常询问在数组 AA 中，比 xx 大的最小值是多大？但是这次蒜头君要求这个数字必须大于 xx，不能等于 xx。

输入格式
第一行输入两个整数 nn 和 mm，分别表示数组的长度和查询的次数。

接下来一行有 nn 个整数 a_ia 
i
​
 。

接下来 mm 行，每行有 11 个整数 xx，表示蒜头君询问的整数。

输出格式
对于每次查询，如果可以找到，输出这个整数。

否则输出 -1−1。

数据范围
1≤n,m≤1e5 0≤x≤1e6

输出时每行末尾的多余空格，不影响答案正确性

样例输入复制
10 5
1 1 1 2 3 5 5 7 8 9
0
1
4
9
10
样例输出复制
1
2
5
-1
-1
```

```c++
#include<cstdio>
#include<cstring>
#include<iostream>
#include<algorithm>

using namespace std;
const int N=1e6+10;
int n,m;
int num[N];
int main(){
    cin>>n>>m;
    for(int i=0;i<n;i++)cin>>num[i];
    
    sort(num,num+n);
    
    while(m--){
        int t;
        cin>>t;
        int l=0,r=n-1;
        while(l<r){
            int mid=l+r>>1;
            if(num[mid]>t){
                r=mid;
            }else{
                l=mid+1;
            }
        }
        if(num[l]>t){
            cout<<num[l]<<endl;
        }else{
            cout<<-1<<endl;
        }
    }
    return 0;
}
```

## 搜索与图论

#### 深度优先搜索（DFS）

#### 宽度优先搜索（BFS）

```c++
#include<cstdio>
#include<cstring>
#include<iostream>
#include<algorithm>
#include<queue>
#define x first
#define y second
using namespace std;
typedef pair<int,int> PII;
const int N=210;
char g[N][N];
int dis[N][N];
int dx[4]={-1,0,1,0},dy[4]={0,1,0,-1};
int n,m;
int T;
int bfs(PII start){
    queue<PII> q;
    memset(dis,-1,sizeof dis);
    dis[start.x][start.y]=0;
    q.push(start);
    while(!q.empty()){
        PII t=q.front();
        q.pop();
        for(int i=0;i<4;i++){
            int a=t.x+dx[i],b=t.y+dy[i];
            if(a>=n||a<0||b>=m||b<0)continue;
            if(g[a][b]=='#')continue;
            if(dis[a][b]!=-1)continue;
            
            if(g[a][b]=='E')return dis[t.x][t.y]+1;
            
            q.push({a,b});
            dis[a][b]=dis[t.x][t.y]+1;
        }
    }
    return -1;
}
int main(){
    cin>>T;
    while(T--){
        cin>>n>>m;
        PII start;
        for(int i=0;i<n;i++){
            for(int j=0;j<m;j++){
                cin>>g[i][j];
                if(g[i][j]=='S'){
                    start={i,j};
                }
            }
        }
        // cout<<start.x<<start.y<<endl;
        int distence=bfs(start);
        if(distence==-1){
            cout<<"oop!"<<endl;
        }else{
            cout<<distence<<endl;
        }
    }
    
    return 0;
}
```



### 求最短路径

#### 单源最短路

##### 所有边权都是正数

###### 朴素Dijkstra算法（稠密图）

​	![在这里插入图片描述](https://img-blog.csdnimg.cn/20210216163038477.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzY4MTU0OQ==,size_16,color_FFFFFF,t_70#pic_center)

```c++
#include<cstdio>
#include<cstring>
#include<iostream>
#include<algorithm>

using namespace std;
const int N=510;
int n,m;
int g[N][N];
int dist[N];
bool st[N];
int dijkstra(){
    memset(dist,0x3f,sizeof dist);
    dist[1]=0;
    for(int i=0;i<n;i++){
        int t=-1;
        for(int j=1;j<=n;j++){
            if(!st[j]&&(t==-1||dist[t]>dist[j])){
                t=j;
            }
        }
        st[t]=true;
        for(int j=1;j<=n;j++){
            dist[j]=min(dist[j],dist[t]+g[t][j]);
        }
    }
    
    if(dist[n]==0x3f3f3f3f) return -1;
    return dist[n];
}
int main(){
    cin>>n>>m;
    memset(g,0x3f,sizeof g);
    while(m--){
        int a,b,c;
        cin>>a>>b>>c;
        g[a][b]=min(g[a][b],c);
    }
    int t=dijkstra();
    cout<<t<<endl;
    
    
    return 0;
}
```



###### 堆优化Dijkstra算法（稀疏图）







##### 存在负权边

###### bellman-ford算法

```
给定一个 n 个点 m 条边的有向图，图中可能存在重边和自环， 边权可能为负数。

请你求出从 1 号点到 n 号点的最多经过 k 条边的最短距离，如果无法从 1 号点走到 n 号点，输出 impossible。

注意：图中可能 存在负权回路 。

输入格式
第一行包含三个整数 n,m,k。

接下来 m 行，每行包含三个整数 x,y,z，表示存在一条从点 x 到点 y 的有向边，边长为 z。

输出格式
输出一个整数，表示从 1 号点到 n 号点的最多经过 k 条边的最短距离。

如果不存在满足条件的路径，则输出 impossible。

数据范围
1≤n,k≤500,
1≤m≤10000,
任意边长的绝对值不超过 10000。

输入样例：
3 3 1
1 2 1
2 3 1
1 3 3
输出样例：
3
```

```c++
#include<cstdio>
#include<cstring>
#include<iostream>
#include<algorithm>

using namespace std;
const int N=510,M=1e4+10;
int n,m,k;
int dist[N],backup[N];
struct Edge{
    int a,b,c;
}edges[M];
void bellman_ford(){
    
    memset(dist,0x3f,sizeof dist);
    dist[1]=0;
    for(int i=0;i<k;i++){
        memcpy(backup,dist,sizeof dist);
        for(int j=0;j<m;j++){
            auto e=edges[j];
            dist[e.b]=min(dist[e.b],backup[e.a]+e.c);
        }
    }
}
int main(){
    cin>>n>>m>>k;
    for(int i=0;i<m;i++){
        int a,b,c;
        cin>>a>>b>>c;
        edges[i]={a,b,c};
    }
    bellman_ford();
    if(dist[n]>0x3f3f3f/2)cout<<"impossible"<<endl;
    else cout<<dist[n]<<endl;
    return 0;
}
```

#### 多源汇最短路

###### 



## 数学

### 数论

#### 试除法求质数

```c++
bool is_prime(int x)
{
    if (x < 2) return false;
    for (int i = 2; i <= x / i; i ++ )
        if (x % i == 0)
            return false;
    return true;
}
```

#### 分解质因数

```
1、题目：
给定n个正整数ai，将每个数分解质因数，并按照质因数从小到大的顺序输出每个质因数的底数和指数。

输入格式
第一行包含整数n。

接下来n行，每行包含一个正整数ai。

输出格式
对于每个正整数ai,按照从小到大的顺序输出其分解质因数后，每个质因数的底数和指数，每个底数和指数占一行。

每个正整数的质因数全部输出完毕后，输出一个空行。

数据范围
1≤n≤100,
1≤ai≤2∗109
输入样例：
2
6
8
输出样例：
2 1
3 1

2 3
```

```c++
#include<cstdio>
#include<cstring>
#include<iostream>
#include<algorithm>

using namespace std;
void divide(int x){
    for(int i=2;i<=x/i;i++){
        if(x%i==0){
            int cnt=0;
            while(x%i==0){
                x/=i;
                cnt++;
            }
            cout<<i<<" "<<cnt<<endl;
        }
    }
    if(x>1)cout<<x<<" "<<1<<endl;
}
int main(){
    int n;
    cin>>n;
    while(n--){
        int x;
        cin>>x;
        divide(x);
        cout<<endl;
    }
    
    return 0;
}
```

#### 筛质数

```
给定一个正整数 n，请你求出 1∼n1∼n 中质数的个数。

输入格式

共一行，包含整数 n。

输出格式

共一行，包含一个整数，表示 1∼n1∼n 中质数的个数。

数据范围

1≤n≤1061≤n≤106

输入样例：
```

##### 欧式筛法

```c++
#include<cstdio>
#include<cstring>
#include<iostream>
#include<algorithm>

using namespace std;
const int N=100010;
int prime[N],cnt;
int n;
bool st[N];
void get_prime(int n){
    for(int i=2;i<=n;i++){
        if(!st[i]){
            prime[cnt++]=i;
            for(int j=i+i;j<=n;j+=i){
                st[j]=true;
            }
        }
    }
}
int main(){
    cin>>n;
    get_prime(n);
    cout<<cnt<<endl;
    return 0;
}
```

##### 线性筛法

```c++
#include <iostream>
#include <algorithm>

using namespace std;

const int N= 1000010;

int primes[N], cnt;
bool st[N];

void get_primes(int n)
{
    for (int i = 2; i <= n; i ++ )
    {
        if (!st[i]) primes[cnt ++ ] = i;
        for (int j = 0; primes[j] <= n / i; j ++ )
        {
            st[primes[j] * i] = true;
            if (i % primes[j] == 0) break;
        }
    }
}

int main()
{
    int n;
    cin >> n;

    get_primes(n);

    cout << cnt << endl;

    return 0;
}
```

#### 试除法求约数

```c++
#include<cstdio>
#include<cstring>
#include<iostream>
#include<algorithm>
#include<vector>

using namespace std;
void get_divisors(int n){
    vector<int>divs;
    for(int i=1;i<=n/i;i++){
        if(n%i==0){
            divs.push_back(i);
            if(i*i!=n)divs.push_back(n/i);
        }
    }
    sort(divs.begin(),divs.end());
    for(auto s:divs){
        cout<<s<<endl;
    }
}
int main(){
    int n;
    cin>>n;
    get_divisors(n);
    
    return 0;
}
```

#### 求约数个数

利用算法基本定理，先分解质因数，然后约数个数就是每个质因数的指数+1的乘积。

```
当然还有更简单的方法，考虑下我们小时候学过的分解质因数的知识。
360=2*2*2*3*3*5=2^3+3^2+5
那么360的约数只能为2^a*3^b*5^c2（a的范围(0-3),b的范围(0-2),c的范围(0-1)），因此360的约数有4*3*2=24个。
具体实现方法：
```

该题求解了100的阶乘的约数的个数。其中使用的哈希map也可以换成简单的map

```c++
#include<cstdio>
#include<cstring>
#include<iostream>
#include<algorithm>
#include<unoredered_map>
using namespace std;

int main(){
    
    map<int,int> mp;
    for(int j=2;j<=100;j++){
        int n=j;
        for(int i=2;i<=n/i;i++){
        if(n%i==0){
            while(n%i==0){
                n/=i;
                mp[i]++;
            }
        }
    }
    if(n>1)mp[n]++;
    }
    for(auto x:mp){
        cout<<x.first<<" "<<x.second+1<<endl;
    }
    long long res=1;
    for(auto x:mp){
        res*=(x.second+1);
    }
    cout<<res;
}
```

#### 求约数的和

![在这里插入图片描述](https://img-blog.csdnimg.cn/1ba4a2a166b5479eba2443902140c529.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ2OTA3NTQ3,size_16,color_FFFFFF,t_70#pic_center)



```c++
#include <iostream>
#include <algorithm>
#include <unordered_map>
#include <vector>

using namespace std;

typedef long long LL;

const int N = 110, mod = 1e9 + 7;

int main()
{
    int n;
    cin >> n;

    unordered_map<int, int> primes;

    while (n -- )
    {
        int x;
        cin >> x;

        for (int i = 2; i <= x / i; i ++ )
            while (x % i == 0)
            {
                x /= i;
                primes[i] ++ ;
            }

        if (x > 1) primes[x] ++ ;
    }

    LL res = 1;
    for (auto p : primes)
    {
        LL a = p.first, b = p.second;
        LL t = 1;
        while (b -- ) t = (t * a + 1) % mod;
        res = res * t % mod;
    }

    cout << res << endl;

    return 0;
}
```



#### 求最大公约数

辗转相除法又叫欧几里得法

```c++
int gcd(int a,int b){
	return b?gcd(b,a%b):a;
}
```

