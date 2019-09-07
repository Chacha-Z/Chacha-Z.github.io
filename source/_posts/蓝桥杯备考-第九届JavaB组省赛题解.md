---
title: 蓝桥杯备考-第九届JavaB组省赛题解
date: 2019-03-21 20:03:31
tags: 
categories: 
    - 蓝桥杯

description: 第九届JavaB组省赛题解
---

## 第几天

<pre>
标题：第几天

2000年的1月1日，是那一年的第1天。
那么，2000年的5月4日，是那一年的第几天？

注意：需要提交的是一个整数，不要填写任何多余内容。
</pre>

    思路：很简单，电脑有自带日期计算器
    注意：1月1日算作第一天，所以最后结果要加1（计算器算出的结果）
        口算：2000年是闰年，31+29+31+20+4 = 125

## 方格计数

<pre>
标题：方格计数

如图p1.png所示，在二维平面上有无数个1x1的小方格。

我们以某个小方格的一个顶点为圆心画一个半径为1000的圆。
你能计算出这个圆里有多少个完整的小方格吗？ 

注意：需要提交的是一个整数，不要填写任何多余内容。
</pre>

[!方格](/p1.png)

    思路：我的妈我在想什么，一开始想半径1000能容纳多少个根号2就有对应多少个方格能够被包括在里面  
    不是的啊！还有在这个n*根号2正方形之外还有可能被包括的   
    [!方格2](/p2.png)
    所以正确的想法应该是，代码实现，遍历一个象限（第一象限），1000边长内，有多少小方格的右上顶点在1000半径内

``` java
		int count = 0;
		for(int i = 1; i <= 1000; ++i){
			for(int j = 1; j <= 1000; ++j){
				if(i*i + j*j <= 1000000){
					count ++;
				}
			}
		}
		System.out.println(count*4); //3137548
```

## 复数幂（未实现快速幂）

<pre>
标题：复数幂

设i为虚数单位。对于任意正整数n，(2+3i)^n 的实部和虚部都是整数。
求 (2+3i)^123456 等于多少？ 即(2+3i)的123456次幂，这个数字很大，要求精确表示。

答案写成 "实部±虚部i" 的形式，实部和虚部都是整数（不能用科学计数法表示），中间任何地方都不加空格，
实部为正时前面不加正号。(2+3i)^2 写成: -5+12i，
(2+3i)^5 的写成: 122-597i

注意：需要提交的是一个很庞大的复数，不要填写任何多余内容。
</pre>

    思路：计算很简单，就算暴力循环123456次好像也可以接受  
    只是，这个数，真的真的真的很庞大，庞大到！我的eclipse显示不出来，显示了两行-，就没啦   
[!复数结果](/plurResult.png)
    原来，只是因为数太大了，赋值控制台这些空白，粘贴到记事本中就可以看到了  
[!复数结果](/plurResult2.png)
    重点：大数计算 BigInteger类
        1. BigInteger.valueOf()
        2. 自带加减乘除方法

``` java
BigInteger a = BigInteger.valueOf(2); 
BigInteger b = BigInteger.valueOf(3); 

BigInteger A = a;
BigInteger B = b;

BigInteger tempA = A;
BigInteger tempB = B;
for(int i = 1; i < 123456; ++i){
    tempA = A;
    tempB = B;
    
    A = tempA.multiply(a).subtract(tempB.multiply(b));
    B = b.multiply(tempA).add(a.multiply(tempB));
}
System.out.println(A);
System.out.println(B);
```
    这还是太暴力了，已经要运行一小会儿了，尝试使用java快速幂优化，占个坑

### 快速幂

[!](https://blog.csdn.net/Du_Mingm/article/details/79201564)

``` java
//递归

int pow(int a,int b)//a^b
{
    if(b==1)
        return a;
    if(b&1)//等价与b%2
        return a*pow(a*a,b/2);
    return pow(a*a,b/2);
}
```

``` java
//非递归
//秦九韶算法按自底向上理解
//或按二进制指数理解
int ans=1,base=a;
    while(b)
    {
        if(b&1)
            ans*=base;
        base*=base;
        b>>=1;//等价b/=2
    }

```

## 测试次数（错误）（已解决）

<pre>
标题：测试次数

x星球的居民脾气不太好，但好在他们生气的时候唯一的异常举动是：摔手机。
各大厂商也就纷纷推出各种耐摔型手机。x星球的质监局规定了手机必须经过耐摔测试，并且评定出一个耐摔指数来，之后才允许上市流通。

x星球有很多高耸入云的高塔，刚好可以用来做耐摔测试。塔的每一层高度都是一样的，与地球上稍有不同的是，他们的第一层不是地面，而是相当于我们的2楼。

如果手机从第7层扔下去没摔坏，但第8层摔坏了，则手机耐摔指数=7。
特别地，如果手机从第1层扔下去就坏了，则耐摔指数=0。
如果到了塔的最高层第n层扔没摔坏，则耐摔指数=n

为了减少测试次数，从每个厂家抽样3部手机参加测试。

某次测试的塔高为1000层，如果我们总是采用最佳策略，在最坏的运气下最多需要测试多少次才能确定手机的耐摔指数呢？

请填写这个最多测试次数。

注意：需要填写的是一个整数，不要填写任何多余内容。
</pre>

    思路：没有思路，一开始想二分法，肯定是错的啊，手机只有三台能够测试  
    注意读题啊！只有三台手机可以用来摔，是测这种手机的，不是测每台手机的  
    在理解这道题之前我们先了解“摔鸡蛋问题”

### 摔鸡蛋问题


## 快速排序

<pre>
标题：快速排序  

以下代码可以从数组a[]中找出第k小的元素。   

它使用了类似快速排序中的分治算法，期望时间复杂度是O(N)的。

请仔细阅读分析源码，填写划线部分缺失的内容。
</pre>

``` java
import java.util.Random;
public class Main{
	public static int quickSelect(int a[], int l, int r, int k) {
		Random rand = new Random();
		int p = rand.nextInt(r - l + 1) + l;
		int x = a[p];
		int tmp = a[p]; a[p] = a[r]; a[r] = tmp;
		int i = l, j = r;
		while(i < j) {
                	while(i < j && a[i] < x) i++;
                	if(i < j) {
                        	a[j] = a[i];
                        	j--;
                	}
                	while(i < j && a[j] > x) j--;
                	if(i < j) {
                        	a[i] = a[j];
                        	i++;
                	}
        	}
        	a[i] = x;
        	p = i;
        	if(i - l + 1 == k) return a[i];
        	if(i - l + 1 < k) return quickSelect( _________________________________ ); //填空
        	else return quickSelect(a, l, i - 1, k);	
	}
	public static void main(String args[]) {
		int [] a = {1, 4, 2, 8, 5, 7};
		System.out.println(quickSelect(a, 0, 5, 4));
	}
}
```

    思路：
        复习一下快速排序的思路：分而治之，选择一个“标兵”，把比他大的全部移到他右边，把比他小的全部移到他左边  
        该代码思路：随机选择一个数，把比他大的全部移到他右边，把比他小的全部移到他左边，最后返回该数最后的位置  
        这个位置即为相对左边界第几大！！（关键）  
        然后!如果这个位置比k大，说明目标数在左边，则递归左边，否则递归右边（注意右边时，k应该是相对左边界的，所以要减该位置表示大小

``` java
if(i - l + 1 < k) return quickSelect(a, i+1, r, k-i+l-1); //填空
```

## 递增三元组

<pre>
标题：递增三元组

给定三个整数数组
A = [A1, A2, ... AN],   
B = [B1, B2, ... BN],   
C = [C1, C2, ... CN]，  
请你统计有多少个三元组(i, j, k) 满足：  

1. 1 <= i, j, k <= N    
2. Ai < Bj < Ck    
 
【输入格式】 
第一行包含一个整数N。 
第二行包含N个整数A1, A2, ... AN。  
第三行包含N个整数B1, B2, ... BN。  
第四行包含N个整数C1, C2, ... CN。  

对于30%的数据，1 <= N <= 100   
对于60%的数据，1 <= N <= 1000  
对于100%的数据，1 <= N <= 100000 0 <= Ai, Bi, Ci <= 100000  

【输出格式】   
一个整数表示答案  
  
【输入样例】   
3   
1 1 1  
2 2 2 
3 3 3  

【输出样例】  
27  
</pre>

    思路：为了不暴力循环，因为我们只需要知道比上一个循环数大的数有多少个，所以对每个三元组从小到大排序  
    还有一个关键问题：怎样累积，乘还是加
    还要注意，不同位置算不同组合

``` java
public class IncreaseTriplet {

	public static void main(String[] args) {
		// TODO 自动生成的方法存根
		int[] test = {2, 2, 2};
		System.out.println(search(test, 1));
		
		Scanner scanner = new Scanner(System.in);
		int N = scanner.nextInt();
		scanner.nextLine();
		int[] A = new int[N];
		int[] B = new int[N];
		int[] C = new int[N];
		
		String[] tempA = scanner.nextLine().split(" ");
		String[] tempB = scanner.nextLine().split(" ");
		String[] tempC = scanner.nextLine().split(" ");
		scanner.close();
		for(int i = 0; i < N; ++i){
			A[i] = Integer.valueOf(tempA[i]);
			B[i] = Integer.valueOf(tempB[i]);
			C[i] = Integer.valueOf(tempC[i]);
		}
		System.out.println(deal(A, B, C));
	}
	
	public static int deal(int[] A, int[] B, int[] C){
		int N = A.length;
		
		Arrays.sort(A);
		Arrays.sort(B);
		Arrays.sort(C);

		int count = 0;  //累积1
		for(int i = 0; i < N; ++i){
			int a = A[i];
			
			int countBC = 0;    //累积2
			for(int j = search(B, a); j < N; ++j){
				int b = B[j];
				
				countBC += N - search(C, b);
				
				System.out.println(search(C, b));
			}
			count += countBC;
		}
		return count;
	}
	
	//返回数组中第一个大于A的数
	public static int search(int[] a, int key){
		int low = 0; 
		int high = a.length-1;
		int mid = (low + high)/2;
		
		while(low < high){
			if(a[mid] < key){
				low = mid+1;
			}else{
				high = mid-1;
			}
			mid = (low + high)/2;
		}
		return low;
	}
}

```

## 螺旋折线

<pre>
标题：螺旋折线

如图p1.pgn所示的螺旋折线经过平面上所有整点恰好一次。  
对于整点(X, Y)，
我们定义它到原点的距离dis(X, Y)是从原点到(X, Y)的螺旋折线段的长度。  

例如dis(0, 1)=3, dis(-2, -1)=9  
给出整点坐标(X, Y)，你能计算出dis(X, Y)吗？

【输入格式】
X和Y 

对于40%的数据，-1000 <= X, Y <= 1000  
对于70%的数据，-100000 <= X， Y <= 100000  
对于100%的数据, -1000000000 <= X, Y <= 1000000000  

【输出格式】
输出dis(X, Y)  

【输入样例】
0 1

【输出样例】
3
</pre>

    思路：找规律，(-m,-m)(m>0)处的点恰好等于所在正方形周长（加若干内圈正方形周长（内圈正方形周长有规律，求和））  
    以(-m, -m)点为参照点，可以计算出该点的长度，同一正方形上的点按规律递减  
    关键：因为输入数据，非常非常大，所以依旧只能使用BigInteter类,真的是看的我头大  


``` java
package season9;

import java.math.BigInteger;

public class SpiralBrokenLine {

	public static void main(String[] args) {
		// TODO 自动生成的方法存根
		//System.out.println(deal(0, 0));
		System.out.println(deal(-1000000000, 990000000));
	}
	
	public static BigInteger deal(int x, int y){
		BigInteger base = BigInteger.valueOf(Math.max(Math.abs(x), Math.abs(y))); //正数(-base, -base)
		BigInteger baseResult = base.multiply(BigInteger.valueOf(8));	//x过大时注意改变存储数据类型

		
		BigInteger distance = BigInteger.valueOf(0);
		if(BigInteger.valueOf(y).equals(base.negate())){
			//distance = baseResult - (x + base);

			distance = baseResult.subtract(BigInteger.valueOf(x).add(base));
		}else if(BigInteger.valueOf(x) == base){
			//distance = baseResult - base*2 - (y + base);
			
			distance = baseResult.subtract(BigInteger.valueOf(2).multiply(base)).subtract(BigInteger.valueOf(y).add(base));
		}else if(BigInteger.valueOf(y) == base){
			//distance = baseResult - 4*base - (base - x);

			distance = baseResult.subtract(BigInteger.valueOf(4).multiply(base)).subtract(base.subtract(BigInteger.valueOf(x)));
		}else if(BigInteger.valueOf(x).equals(base.negate())){	//不能用==号
			//distance = baseResult - 6*base - (base - y);
			distance = baseResult.subtract(BigInteger.valueOf(6).multiply(base)).subtract(base.subtract(BigInteger.valueOf(y)));
		}
		//distance + 8*(base-1) + (base-2)*(base-1)*8/2;

		return distance.add(BigInteger.valueOf(8).multiply(base.subtract(BigInteger.valueOf(1)))).add(base.subtract(BigInteger.valueOf(2)).multiply(base.subtract(BigInteger.valueOf(1))).multiply(BigInteger.valueOf(8)).divide(BigInteger.valueOf(2))); 
	}
}

```

## 日志统计（未解决）

> 标题：日志统计  
小明维护着一个程序员论坛。现在他收集了一份"点赞"日志，日志共有N行。其中每一行的格式是：  
ts id    
表示在ts时刻编号id的帖子收到一个"赞"。    
现在小明想统计有哪些帖子曾经是"热帖"。  
如果一个帖子曾在任意一个长度为D的时间段内收到不少于K个赞，小明就认为这个帖子曾是"热帖"。    
具体来说，如果存在某个时刻T满足该帖在[T, T+D)这段时间内(注意是左闭右开区间)收到不少于K个赞，该帖就曾是"热帖"。    
给定日志，请你帮助小明统计出所有曾是"热帖"的帖子编号。   

> 【输入格式】  
第一行包含三个整数N、D和K。    
以下N行每行一条日志，包含两个整数ts和id。   
对于50%的数据，1 <= K <= N <= 1000   
对于100%的数据，1 <= K <= N <= 100000 0 <= ts <= 100000 0 <= id <= 100000   
【输出格式】  
按从小到大的顺序输出热帖id。每个id一行。    
【输入样例】  
7 10 2    
0 1   
0 10     
10 10   
10 1   
9 1  
100 3   
100 3   
【输出样例】  
1   
3   

**思路**：看了人家的解答还觉得蛮好解得...最简单就是排序嘛按id处理
扩展：尺取法

``` java
//比较好理解的方法，可是当数据很大的时候很困难（涉及排序）
package season9;

import java.util.Arrays;
import java.util.Scanner;

public class CountFever
{
	public static void main(String args[])
	{
		int n,d,k;
		Scanner sc=new Scanner(System.in);
		n=sc.nextInt();
		d=sc.nextInt();
		k=sc.nextInt();
		Node arr[]=new Node[n];
		for(int i=0;i<n;i++)
			arr[i]=new Node(sc.nextInt(),sc.nextInt());
		Arrays.sort(arr);	//先按id排序，再按ts升序排序
		
//		for(int i = 0; i < n; ++i){
//			System.out.println(arr[i].ts + " " + arr[i].id);
//		}
		int curid=arr[0].id;
		int added=0;
		for(int i=0;i<n;i++)
		{			
			if(i+k-1<n&&arr[i+k-1].id==curid&&arr[i+k-1].ts-arr[i].ts<d&&added==0)
				{System.out.println(curid);added=1;}
			else if(arr[i].id!=curid)
			{
				curid=arr[i].id;
				added=0;
				i=i-1;
			}
		}
	
	}
}
class Node implements Comparable<Node>
{
	int ts,id;
	Node(int a,int b)
	{
		ts=a;
		id=b;
	}
	
	@Override
	public int compareTo(Node o) {
		if(id==o.id)
			return ts-o.ts;
		else
			return id-o.id;
	}
	
}
```

### 尺取法
> 有n个正整数组成一个序列，给定整数S，求长度最短的连续序列，使得他们的和大于等于S
> 设输入的序列为A[i], i=1..n, 构造前缀数组B[j], j=1..n, B[j]=B[j-1]+A[j], 规定B[0]=0, 当B[j]-B[i-1]>=s的时候i增加  
直至B[j]-B[i]<s, 然后更新最短的满足条件的序列的长度j-i+1，复杂度为O（n）

``` java
#include<stdio.h>
#include<string.h>
#include<math.h>
#include<queue>
#include<algorithm>
#include<time.h>
#include<stack>
using namespace std;
#define N 1200000
#define INF 0x3f3f3f3f

int dp[N];
int a[N];

int main()
{
    int n,m,T,i,j;

    scanf("%d", &T);

    while(T--)
    {
        scanf("%d %d", &n, &m);
        memset(dp,0,sizeof(dp));

        for(i=1;i<=n;i++)
        {
            scanf("%d", &a[i]);
            dp[i]=dp[i-1]+a[i];
        }

        int minn=INF,i=1;;
        for(j=1;j<=n;j++)
        {
             if(dp[j]-dp[i-1]<m)
                continue ;
             while(dp[j]-dp[i]>=m)
                i++;
             minn=min(minn,j-i+1);
        }

      if(minn==INF)
        printf("0\n");
      else
        printf("%d\n", minn);
    }
    return 0;
}
```

``` java
//尺取法做这道题
#include<iostream>
#include<algorithm>
#include<vector>
using namespace std;
const int maxn=1e5+5;
int n,d,k;
vector<int> journal[maxn];

void judge(vector<int>& vec,int id){
    int Size=vec.size();
    if(Size<k) return ;//点赞条数小于k,肯定不能上热帖
    sort(vec.begin(),vec.end());
    int st=0,en=1;
    int cnt=0;
    while(st<=en&&en<Size){
        if(vec[en]-vec[st]<d){
            cnt=max(cnt,en-st+1);
            en++;
        }
        else{
            st++;
        }
    }
//    cout<<"cnt="<<cnt<<" ";

    if(cnt>=k){
        cout<<id<<endl;
    }
}
int main(){
    cin>>n>>d>>k;
    for( int i=0; i<n; i++ ){
        int ts,id;
        cin>>ts>>id;
        journal[id].push_back(ts);
    }
    for( int i=0; i<maxn; i++ ){
        judge(journal[i],i);
    }

    return 0;
}
```

## 全球变暖

<pre>
标题：全球变暖
你有一张某海域NxN像素的照片，"."表示海洋、"#"表示陆地，如下所示：
.......
.##....
.##....
....##.
..####.
...###.
.......
其中"上下左右"四个方向上连在一起的一片陆地组成一座岛屿。例如上图就有2座岛屿。  
由于全球变暖导致了海面上升，科学家预测未来几十年，岛屿边缘一个像素的范围会被海水淹没。具体来说如果一块陆地像素与海洋相邻(上下左右四个相邻像素中有海洋)，它就会被淹没。  
例如上图中的海域未来会变成如下样子：

.......
.......
.......
.......
....#..
.......
.......

请你计算：依照科学家的预测，照片中有多少岛屿会被完全淹没。  

【输入格式】
第一行包含一个整数N。  (1 <= N <= 1000)  
以下N行N列代表一张海域照片。  

照片保证第1行、第1列、第N行、第N列的像素都是海洋。  

【输出格式】
一个整数表示答案。

【输入样例】
7 
.......
.##....
.##....
....##.
..####.
...###.
.......  

【输出样例】
1  
</pre>

    思路：不是很懂他的题目描述的输出和输出样例竟然不是一个东西  
    题目很简单，遍历数组，如果周围（上下左右）有海则被淹没  
    且因为题目保证“照片保证第1行、第1列、第N行、第N列的像素都是海洋”，所以不用判断边界问题  

``` java
Scanner scanner = new Scanner(System.in);
int N = scanner.nextInt();
scanner.nextLine();
char[][] island = new char[N][N];
for(int i = 0; i < N; ++i){
    String str = scanner.nextLine();
    for(int j = 0; j < N; ++j){
        island[i][j] = str.charAt(j);
    }
}
scanner.close();

int countAll = 0;
int count = 0;
for(int i = 1; i < N-1; ++i){
    for(int j = 1; j < N-1; ++j){
        if(island[i][j] == '#'){
            countAll++;
            boolean flag = false;
            
            if(island[i-1][j] == '.' || island[i][j-1] == '.' || island[i][j+1] == '.' || island[i+1][j] == '.'){
                flag = true;
            }
            
            if(flag){
                count++;
            }
        }
    }
}

System.out.println(countAll - count);
```

## 堆的计数（未解决）

<pre>
标题：堆的计数

我们知道包含N个元素的堆可以看成是一棵包含N个节点的完全二叉树。  
每个节点有一个权值。对于小根堆来说，父节点的权值一定小于其子节点的权值。  

假设N个节点的权值分别是1~N，你能求出一共有多少种不同的小根堆吗？  

例如对于N=4有如下3种：

    1
   / \
  2   3
 /a
4

    1
   / \
  3   2
 /
4

    1
   / \
  2   4
 /
3

由于数量可能超过整型范围，你只需要输出结果除以1000000009的余数。  

【输入格式】
一个整数N。  
对于40%的数据，1 <= N <= 1000  
对于70%的数据，1 <= N <= 10000  
对于100%的数据，1 <= N <= 100000

【输出格式】
一个整数表示答案。  

【输入样例】
4  

【输出样例】
3
</pre>