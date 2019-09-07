---
title: 蓝桥杯备考-第六届JavaB组省赛题解
date: 2019-03-21 21:33:37
tags: 
categories: 
    - 蓝桥杯

description: 第九届JavaB组省赛题解
---


## 三角形面积

> 三角形面积  
如【图1】所示。图中的所有小方格面积都是1。  
那么，图中的三角形面积应该是多少呢？   
请填写三角形的面积。不要填写任何多余内容或说明性文字。  


**思路**： 简单到怀疑自己；28


## 立方变自身

> 立方变自身  
观察下面的现象,某个数字的立方，按位累加仍然等于自身。  
1^3 = 1   
8^3  = 512    5+1+2=8  
17^3 = 4913   4+9+1+3=17  
...  
请你计算包括1,8,17在内，符合这个性质的正整数一共有多少个？  
请填写该数字，不要填写任何多余的内容或说明性的文字。

**思路**：循环；  
问题：怎样判断结束条件，我现在的思路就是把它全部输出来，直到不变

```java
package season6;

public class Tow_TripleSelf {

	public static void main(String[] args) {
		// TODO 自动生成的方法存根
		
		int count = 0;
		for(int i = 1; ; ++i){	//怎样判断结束条件，我现在的思路就是把它全部输出来，直到不变
			if(i == selfAdd(Math.pow(i, 3))){
				count++;
			}
			System.out.print(i + " ");
			System.out.println(count);
		}
		//1、8、17、18、26、27
		//6
	}
	
	public static int selfAdd(double x){
		int sum = 0;
		
		while(x != 0){
			sum += x%10;
			x /= 10;
		}
		
		return sum;
	}

}

```


## 三羊献瑞

> 三羊献瑞  
观察下面的加法算式：  

<pre>
      祥 瑞 生 辉
  +   三 羊 献 瑞
-------------------
   三 羊 生 瑞 气
</pre>


> 其中，相同的汉字代表相同的数字，不同的汉字代表不同的数字。  
请你填写“三羊献瑞”所代表的4位数字（答案唯一），不要填写任何多余内容。


**思路**： 挺简单的一道题，因为条件写错了o写成0调了一会儿，注意判断个位数和其他数字都不同

``` java
package season6;

public class Three_ChineseExpression {

	public static void main(String[] args) {
		// TODO 自动生成的方法存根
		for(int l = 1; l <= 9; ++l){ //祥
			for(int m = 0; m <= 9; ++m){ //瑞
				if(m == l) continue;
				for(int n = 0; n <= 9; ++n){ //生
					if(n == m || n == l) continue;
					for(int o = 0; o <= 9; ++o){ //辉
						if(o == l || o == m || o == n) continue;
						
						for(int p = 1; p <= 9; ++p){	//三
							if(p == l || p == m || p == n || p== o) continue;
							for(int q = 0; q <= 9; ++q){	//羊
								if(q == l || q == m || q == n || q== o || q == p) continue;
								for(int r = 0; r <= 9; ++r){	//献
									if(r == l || r == m || r == n || r== o || r == p || r == q) continue;
									
									int a = l*1000+m*100+n*10+o;
									int b = p*1000+q*100+r*10+m;
									
									int c = a+b;
									
									if(c/10000 == p && (c/1000)%10 == q &&
											(c/100)%10 == n && (c/10)%10 == m &&
											c%10 != l && c%10 != m && c%10 != n && c%10 != o && c%10 != p && 
											c%10 != q && c%10 != r ){
										System.out.println(p + " " + q + " " + r + " " + m);	//1 0 8 5
										System.out.println(c);	//10652
									}
								}
							}
						}
					}
				}
			}
		}
	}

}

```

``` java
//DFS
public class 三羊献瑞 {
	
	public static void main(String args[]){
		int a[]=new int[8];
		for(int i=0;i<8;i++){
			a[i]=0;
		}
		fun(a,0);
		
	}
	public static void fun(int a[],int n){
		if(n==8){
			if(check_sum(a)){
			
			System.out.println(a[0]+""+a[1]+""+a[2]+""+a[3]);
			return;
			}
		}else{
			for(int i=0;i<10;i++){
				a[n]=i;	//设置当前位为i
				if(check(a,n)) fun(a,n+1);	//不是全排列不用回溯（什么时候需要回溯？）
			}
		}
	}
	public static boolean check(int a[],int n){
		boolean flag=true;
		if(n==0){
			if(a[n]==0) flag=false;
		}else{
			
			for(int i=0;i<n;i++){
				if(a[i]==a[n]){
					flag=false;
					break;
				}
			}
			if(n==4 && a[n]==0) flag=false;
				
			
		}
		return flag;
	}
	public static boolean check_sum(int a[]){
		int x=1000*a[4]+100*a[3]+10*a[5]+a[6];
		int y=1000*a[0]+100*a[1]+10*a[2]+a[3];
		int z=10000*a[0]+1000*a[1]+100*a[5]+10*a[3]+a[7];
		if((x+y)==z){
			return true;
		}else{
			return false;
		}
	}
 
}
```

## 循环节长度（错误）（已解决）

> 循环节长度  
两个整数做除法，有时会产生循环小数，其循环部分称为：循环节。  
比如，11/13=6=>0.846153846153.....  其循环节为[846153] 共有6位。   
下面的方法，可以求出循环节的长度。  
请仔细阅读代码，并填写划线部分缺少的代码。  

``` java
	public static int f(int n, int m)
	{
		n = n % m;	
		Vector v = new Vector();
		
		for(;;)
		{
			v.add(n);
			n *= 10;
			n = n % m;
			if(n==0) return 0;
			if(v.indexOf(n)>=0)  _________________________________ ;  //填空
		}
	}
```

> 注意，只能填写缺少的部分，不要重复抄写已有代码。不要填写任何多余的文字。

**思路**：凑出来的，不是很懂这个怎么求的，看代码觉得应该返回一个值这个值就应该是所求的长度
能返回些什么值呢，就凑出来了，v.size()，结果当然是错的  
这串代码的思路是，首先要知道怎么求小数部分，余数乘以10除以除数的商是小数部分，因为每次对应取余数的m都相同，只要当余数重复出现时，商就会重复，即为循环小数部分。  
v.indexof(n)即为判断余数是否重复，因为重复位置不一定是在第一个，所以当前长度还要减去第一次出现重复的位置


``` java
if(v.indexOf(n)>=0)  return v.size();  //填空
```

## 九数组分数（错误）（已解决）

> 九数组分数  
1,2,3...9 这九个数字组成一个分数，其值恰好为1/3，如何组法？  
下面的程序实现了该功能，请填写划线部分缺失的代码。  

``` java
public class A
{
	public static void test(int[] x)
	{
		int a = x[0]*1000 + x[1]*100 + x[2]*10 + x[3];
		int b = x[4]*10000 + x[5]*1000 + x[6]*100 + x[7]*10 + x[8];		
		if(a*3==b) System.out.println(a + " " + b);
	}
	
	public static void f(int[] x, int k)
	{
		if(k>=x.length){
			test(x);
			return;
		}
		
		for(int i=k; i<x.length; i++){
			{int t=x[k]; x[k]=x[i]; x[i]=t;}
			f(x,k+1);
			_______________________________________       // 填空
		}
	}
	
	public static void main(String[] args)
	{
		int[] x = {1,2,3,4,5,6,7,8,9};		
		f(x,0);
	}
}
```

> 注意，只能填写缺少的部分，不要重复抄写已有代码。不要填写任何多余的文字。

``` java
{int t=x[k]; x[k]=x[i]; x[i]=t;}  // 填空
```

**思路**：没有思路；能够想到这道题肯定是个递归，也有循环条件。能够想到是全排列，然后在test(x)判断输出；  
所以我尝试在划线处填入test(x)，但是错了，啥也输不出来；又将划线处x数组打印出来，发现到这一步并不是全排列，有漏掉的情况；  
然后，就没有然后了；  
这是一个递归全排列，占个坑  

### 递归全排列

``` java
package season6;

import java.util.Arrays;

public class RecursionPerm {

	public static void main(String[] args) {
		// TODO 自动生成的方法存根
		int[] x = {1,2,3,4,5,6,7,8,9};	
		perm(x, 0);
	}
	
	
	public static void perm(int[] x, int k){
		
		if(k >= x.length){
			System.out.println(Arrays.toString(x));
			return ;
		}
		
		for(int i = k; i < x.length; ++i){
			swap(x, k, i);
			perm(x, k+1);
			swap(x, k, i);
		}
	}
	
	public static void swap(int[] x, int i, int j){
		int temp = x[i];
		x[i] = x[j];
		x[j] = temp;
	}

}

```



## 加法变乘法

> 加法变乘法  
我们都知道：1+2+3+ ... + 49 = 1225  
现在要求你把其中两个不相邻的加号变成乘号，使得结果为2015  
比如：  
1+2+3+...+10*11+12+...+27*28+29+...+49 = 2015  
就是符合要求的答案。  
请你寻找另外一个可能的答案，并把位置靠前的那个乘号左边的数字提交（对于示例，就是提交10）。  
注意：需要你提交的是一个整数，不要填写任何多余的内容。  

**思路**：先用数学转换，49个数之和可以求得为1225，拿两对数来相乘（m/m+1、n/n+1）剩下的和为1225-m-m-1-n-n-1  
剩下的和加上两对数的乘积等于2015， 化简可以得到算式，在遍历对m、n取值

``` java
		for(int i = 1; i <= 47; ++i){
			for(int j = i+2; j <= 48; ++j){
				if(i*i-i + j*j-j == 792){
					System.out.println(i + " " + j);
					//10 27
					//16 24
				}
			}
		}
```

## 牌型种数

> 牌型种数  
小明被劫持到X赌城，被迫与其他3人玩牌。  
一副扑克牌（去掉大小王牌，共52张），均匀发给4个人，每个人13张。  
这时，小明脑子里突然冒出一个问题：  
如果不考虑花色，只考虑点数，也不考虑自己得到的牌的先后顺序，  
自己手里能拿到的初始牌型组合一共有多少种呢？  

请填写该整数，不要填写任何多余的内容或说明文字。  

**思路**：数学太差，甚至想重学高中数学，只能考虑暴力解法  
1-13点数，每个点数4张牌，考虑暴力循环，对每张牌出现的次数进行循环，之和等于13

``` java
//int countAll = 0;
int count = 0;
for(int a = 0; a <= 4; ++a){	//1
	for(int b = 0; b <= 4; ++b){	//2
		for(int c = 0; c <= 4; ++c){	//3
			for(int d = 0; d <= 4; ++d){	//4
				for(int e = 0; e <= 4; ++e){	//5
					for(int f = 0; f <= 4; ++f){	//6
						for(int g = 0; g <= 4; ++g){	//7
							for(int h = 0; h <= 4; ++h){	//8
								for(int i = 0; i <= 4; ++i){	//9
									for(int j = 0; j <= 4; ++j){	//10
										for(int k = 0; k <= 4; ++k){	//11
											for(int l = 0; l <= 4; ++l){	//12
												for(int m = 0; m <= 4; ++m){	//13
													countAll++;
													if(a+b+c+d+e+f+g+h+i+j+k+l+m == 13){
														count++;
													}
												}
											}
										}
									}
								}
							}
						}
					}
				}
			}
		}
	}
}
//System.out.println(countAll);//1220703125
System.out.println(count);//3598180
```
``` java
//DFS

public class Seven_dfsOrder {

	private static int ans = 0;
	public static void main(String[] args) {
		// TODO 自动生成的方法存根
		dfs(0, 0);
		System.out.println(ans);
	}
	
	public static void dfs(int step, int count){
		if(count > 13){
			return ;
		}
		
		if(step == 13){
			if(count == 13){
				ans++;
			}
			return ;
		}
		
		for(int n = 0; n <= 4; ++n){
			count += n;
			dfs(step+1, count);
			count -= n;
		}
	}

}

```


## 饮料换购

> 饮料换购
乐羊羊饮料厂正在举办一次促销优惠活动。乐羊羊C型饮料，  
凭3个瓶盖可以再换一瓶C型饮料，并且可以一直循环下去，但不允许赊账。  
请你计算一下，如果小明不浪费瓶盖，尽量地参加活动，  
那么，对于他初始买入的n瓶饮料，最后他一共能得到多少瓶饮料。  
输入：一个整数n，表示开始购买的饮料数量（0<n<10000）  
输出：一个整数，表示实际得到的饮料数  

> 例如：  
用户输入：  
100  
程序应该输出：  
149  
用户输入：  
101  
程序应该输出：  
151  

**思路**：使用模拟这个过程就好了，三瓶三瓶计算，然后再加一瓶

``` java
Scanner scanner = new Scanner(System.in);

int N = scanner.nextInt();

int nowHave = N;

int countBottle = N;
int count = 0;
while(nowHave != 0){
	//System.out.println(nowHave);
	count++;
	nowHave--;
	
	if(count == 3){
		nowHave++;
		//System.out.println(nowHave);
		countBottle++;
		count = 0;
	}
}

System.out.println(countBottle);
```

