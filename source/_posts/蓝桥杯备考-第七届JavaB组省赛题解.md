---
title: 蓝桥杯备考-第七届JavaB组省赛题解
date: 2019-03-21 15:48:27
tags: 
categories: 
    - 蓝桥杯

description: 非常暴力
---

## 煤球数目

> 煤球数目
有一堆煤球，堆成三角棱锥形。具体：  
第一层放1个，  
第二层3个（排列成三角形），  
第三层6个（排列成三角形），  
第四层10个（排列成三角形），  
....  
如果一共有100层，共有多少个煤球？  
请填表示煤球总数目的数字。  
注意：你提交的应该是一个整数，不要填写任何多余的内容或说明性文字。

    画半天（为了确定规律，比赛的时候就要不证明了），其实从前面几个数字能看出来规律，{1, 3, 6, 10...}，分别为前一层{+2, +3, +4...}

``` java
int sum = 0;
int step = 1;
int count = 1;
for(int i = 1; i <= 100; ++i){
    sum += count;
    step++;
    count += step;
}

System.out.println(sum);//171700
```

## 生日蜡烛

> 生日蜡烛  
某君从某年开始每年都举办一次生日party，并且每次都要吹熄与年龄相同根数的蜡烛。  
现在算起来，他一共吹熄了236根蜡烛。  
请问，他从多少岁开始过生日party的？  
请填写他开始过生日party的年龄数。  
注意：你提交的应该是一个整数，不要填写任何多余的内容或说明性文字。

    思路：分别循环确定起始年龄和结束年龄，然后再遍历一次求区间和（怎么有点像暴力求最大子列和；看了看，我为什么要从后面遍历？这样就不能利用前一次循环的结果了，脑子不太好用）

``` java
int s = 0;
int e = 0;

outer: for(int begin = 1; begin <= 100; ++begin){
    for(int end = 100; end >= begin; --end){
        int sum = 0;
        for(int i = begin; i <= end; ++i){
            sum += i;
        }
        if(sum == 236){
            s = begin;
            e = end;
            break outer;
        }
    }
}

System.out.println(s + " - " + e);
//26 - 33
```

    改一改，end从begin开始循环

``` java
outer: for(int begin = 1; begin <= 100; ++begin){
    int sum = begin;
    for(int end = begin+1; end <= 100; ++end){
        sum += end;
        if(sum == 236){
            s = begin;
            e = end;
            break outer;
        }
        
        if(sum > 236){
            break;
        }
    }
}
```
    这样子退出循环有点想GOTO，是不是不太好，改一改，试一试用标志变量退出循环。我去，找到了就直接打印啊，何必哪个数来存，或者还要担心+-1的问题


``` java
int begin = 1, end = begin;
boolean flag = true;
for(begin = 1; begin < 100 && flag; ++begin){
    int sum = begin;
    end = begin+1;
    while(true){
        sum += end;
        if(sum == 236){
            System.out.println(begin + " - " + end);
            //26 - 33
            flag = false;
            break;
        }
        
        if(sum > 236){
            break;
        }
        end++;
    }
    
}
```

## 凑算式

> 凑算式  
<pre>
     B      DEF
A + --- + ------- = 10
     C      GHI
</pre>
	 
> 这个算式中A~I代表1~9的数字，不同的字母代表不同的数字。  
比如：  
6+8/3+952/714 就是一种解法，  
5+3/1+972/486 是另一种解法。  
这个算式一共有多少种解法？   
注意：你提交应该是个整数，不要填写任何多余的内容或说明性文字。

    暴力，循环ABCDEFGHI分别取一到九，排除相等的情况
    注意：因为整数除整数等于整数，所以注意数据类型转换
	另一种方法：DFS - 扩展基础，dfs全排列1-9

``` java
package season7;

public class Three_ExpressionTen {

	public static void main(String[] args) {
		// TODO 自动生成的方法存根
		int count = 0;
		for(int a = 1; a <= 9; ++a){
			for(int b = 1; b <= 9; ++b){
				for(int c = 1; c <= 9; ++c){
					for(int d = 1; d <= 9; ++d){
						for(int e = 1; e <= 9; ++e){
							for(int f = 1; f <= 9; ++f){
								for(int g = 1; g <= 9; ++g){
									for(int h = 1; h <= 9; ++h){
										for(int i = 1; i <= 9; ++i){
											
											if(a!=b && a!=c && a!=d && a!=e && a!=f && a!=g && a!=h && a!=i){
												if(b!=c && b!=d && b!=e && b!=f && b!=g && b!=h &&b!=i){
													if(c!=d && c!=e && c!=f && c!=g && c!=h && c!=i){
														if(d!=e && d!=f && d!=g && d!=h && d!=i){
															if(e!=f && e!=g && e!=h && e!=i){
																if(f!=g && f!=h && f!=i){
																	if(g!=h && g!=i){
																		if(h!=i){
																			if(a + (float)b/c + ((float)((d*100)+(e*10)+f))/((g*100)+(h*10)+i) == 10){
																				count++;
																				//System.out.println(a + " " + b + " " + c + " " + ((d*100)+(e*10)+f) + " " + ((g*100)+(h*10)+i));
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
					}
				}
			}
		}
		System.out.println(count);//29
	}
}

```

    还有一种暴力循环模板，效率应该会好那么一点点点点
``` java
for(int a = 0; a <= 9; ++a){
    for(int b = 0; b <= 9; ++b){
        if(b == a) continue;
        for(int c = 0; c <= 9; ++c){
            if(c == a || c == b) continue;
            for(int d = 0; d <= 9; ++d){
                if(d == a || d == b || d == c) continue;
                for(int e = 0; e <= 9; ++e){
                    if(e == a || e == b || e == c || e == d) continue;
                    for(int f = 0; f <= 9; ++f){
                        if(f == a || f == b || f == c || f == d || f == e) continue;
                        for(int g = 0; g <= 9; ++g){
                            if(g == a || g == b || g == c || g == d || g == e || g == f) continue;
                            for(int h = 0; h <= 9; ++h){
                                if(h == a || h == b || h == c || h == d || h == e || h == f || h == g) continue;
                                for(int i = 0; i <= 9; ++i){
                                    if(i == a || i == b || i == c || i == d || i == e || i == f || i == g || i == h) continue;
                                    for(int j = 0; j <= 9; ++j){
                                        if(j == a || j == b || j == c || j == d || j == e || j == f || j == g || j == h || j == i) continue;
                                            //OPERATION
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
```

### 全排列

> 将1-9全排列

``` java
package dfs;

import java.util.Arrays;

public class ArrangeOneToNine {
	
	private static int[] a = new int[9];
	private static boolean[] visited = new boolean[10];

	public static void main(String[] args) {
		// TODO 自动生成的方法存根
		dfs(0);
	}
	
	public static void dfs(int step){
		
		if(step == 9){
			System.out.println(Arrays.toString(a));
			return ;
		}
		
		for(int i = 1; i <= 9; ++i){
			if(visited[i] == false){
				visited[i] = true;
				a[step] = i;
				dfs(step+1);
				visited[i] = false;
			}
		}
	}

}

```

> DFS全排列解决这道题

``` java
	package season7;

import java.util.Arrays;

public class Three_DFS {

	private static int[] a = new int[10];
	private static boolean[] visited = new boolean[10];
	private static int count = 0;
	
	public static void main(String[] args) {
		// TODO 自动生成的方法存根
		dfs(1);
		System.out.println(count);
	}
	
	public static void dfs(int step){
		
		if(step == 10){
			if(check()){
				count++;
			}
			//System.out.println(Arrays.toString(a));
			return ;
		}
		
		for(int i = 1; i <= 9; ++i){
			if(visited[i] == false){
				visited[i] = true;
				a[step] = i;
				dfs(step+1);
				visited[i] = false;
			}
		}
	}
	
	public static boolean check(){
		double q=a[1];
        double w=a[2]*1.00/a[3];
        double e=(a[4]*100+a[5]*10+a[6])*1.00/(a[7]*100+a[8]*10+a[9]);
        if(q+w+e==10.00){
            return true;
        } else {
            return false;
        }
	}

}

```

## 分小组

> 分小组  
9名运动员参加比赛，需要分3组进行预赛。
有哪些分组的方案呢？  
我们标记运动员为 A,B,C,... I
下面的程序列出了所有的分组方法。  
该程序的正常输出为：  
ABC DEF GHI  
ABC DEG FHI  
ABC DEH FGI  
ABC DEI FGH  
ABC DFG EHI  
ABC DFH EGI  
ABC DFI EGH  
ABC DGH EFI  
ABC DGI EFH  
ABC DHI EFG  
ABC EFG DHI  
ABC EFH DGI  
ABC EFI DGH  
ABC EGH DFI  
ABC EGI DFH  
ABC EHI DFG  
ABC FGH DEI  
ABC FGI DEH  
ABC FHI DEG  
ABC GHI DEF  
ABD CEF GHI  
ABD CEG FHI  
ABD CEH FGI  
ABD CEI FGH  
ABD CFG EHI  
ABD CFH EGI  
ABD CFI EGH  
ABD CGH EFI  
ABD CGI EFH  
ABD CHI EFG  
ABD EFG CHI  
..... (以下省略，总共560行)。

``` java
public class A
{
	public static String remain(int[] a)
	{
		String s = "";
		for(int i=0; i<a.length; i++){
			if(a[i] == 0) s += (char)(i+'A');
		}	
		return s;
	}
	
	public static void f(String s, int[] a)
	{
		for(int i=0; i<a.length; i++){
			if(a[i]==1) continue;
			a[i] = 1;
			for(int j=i+1; j<a.length; j++){
				if(a[j]==1) continue;
				a[j]=1;
				for(int k=j+1; k<a.length; k++){
					if(a[k]==1) continue;
					a[k]=1;
					System.out.println(________);  //填空位置
					a[k]=0;
				}
				a[j]=0;
			}
			a[i] = 0;
		}
	}
	
	public static void main(String[] args)
	{
		int[] a = new int[9];		
		a[0] = 1;
		
		for(int b=1; b<a.length; b++){
			a[b] = 1;
			for(int c=b+1; c<a.length; c++){
				a[c] = 1;
				String s = "A" + (char)(b+'A') + (char)(c+'A');
				f(s,a);
				a[c] = 0;
			}
			a[b] = 0;
		}
	}
}
```

> 仔细阅读代码，填写划线部分缺少的内容。  
注意：不要填写任何已有内容或说明性文字。

    代码填空题，把代码复制进ECLIPSE，删除横线；
    这套题真的很坑啊！九个人分三组的结果应该是280，我纠结好久数学怎样排列组合；
    说一下代码思路：固定A在第一个不变，当前遍历位置置为1；  
    主要看一下remian()函数，发现在给出来的代码中没有一个地方用到了remain函数，试着在填空处将s+remain()输出，remain()是输出遍历为1之外的位置的值，s是main函数里遍历得到的三个字母，一共输出6个字母，发现就f函数遍历为1的三个位置的值没有输出，根据给出实例，找到应该输出的s remain和f遍历出的位置关系，填入

``` java
System.out.println(s + " "+ (char)('A'+i)+(char)('A'+j)+(char)('A'+k) + " " + remain(a));  //填空位置
```

## 抽签 

> 抽签  
X星球要派出一个5人组成的观察团前往W星。  
其中：  
A国最多可以派出4人。  
B国最多可以派出2人。  
C国最多可以派出2人。  
....    
那么最终派往W星的观察团会有多少种国别的不同组合呢？  
下面的程序解决了这个问题。  
数组a[] 中既是每个国家可以派出的最多的名额。  
程序执行结果为：  
DEFFF  
CEFFF  
CDFFF
CDEFF
CCFFF
CCEFF
CCDFF
CCDEF
BEFFF
BDFFF
BDEFF
BCFFF
BCEFF
BCDFF
BCDEF  
....  
(以下省略，总共101行)

```java
public class A
{
	public static void f(int[] a, int k, int n, String s)
	{
		if(k==a.length){ 
			if(n==0) System.out.println(s);
			return;
		}
		
		String s2 = s;
		for(int i=0; i<=a[k]; i++){
			_____________________________;   //填空位置
			s2 += (char)(k+'A');
		}
	}
	
	public static void main(String[] args)
	{
		int[] a = {4,2,2,1,1,3};
		
		f(a,0,5,"");
	}
}
```
> 仔细阅读代码，填写划线部分缺少的内容。  
注意：不要填写任何已有内容或说明性文字。

    思路：注意理解k和n分别是什么，k是当前循环国家（所以f中循环是在当前循环国家的人数内循环），n是需要派出的人数  
    别忘了这是一道递归题（这很明显，并且存在递归结束条件），使用递归的思想思考，当前k国派出i个人后，下一个循环国家k+1国，还需要派出n-i个人。  
    注意不要走远了，一般代码填空题就一行代码  


``` java
f(a, k+1, n-i, s2); //填空位置
```

## 方格填数

> 方格填数  
如下的10个格子
<pre>
   +--+--+--+
   |  |  |  |
+--+--+--+--+
|  |  |  |  |
+--+--+--+--+
|  |  |  |
+--+--+--+
</pre>
> 填入0~9的数字。要求：连续的两个数字不能相邻。  
（左右、上下、对角都算相邻）  
一共有多少种可能的填数方案？  
请填写表示方案数目的整数。  
注意：你提交的应该是一个整数，不要填写任何多余的内容或说明性文字。


    填空题
    想到了K好数问题，往这个方向思考半天无果（K好数是一维问题，这个是二维）
    暴力循环：什么二维数组，不要想了；为每一个格子设置一个变量来表示，每个变量分别取值0-9（确保不一样），然后当前变量是否和它的相邻变量连续  
	第二种方法：同样是一个排列全部数字的dfs

``` java
package season7;

public class Six_FillGrid {

	public static void main(String[] args) {
		// TODO 自动生成的方法存根
		int[][] grid = new int[3][4];
		int count = 0;
		for(int a = 0; a <= 9; ++a){
			for(int b = 0; b <= 9; ++b){
				if(b == a) continue;
				for(int c = 0; c <= 9; ++c){
					if(c == a || c == b) continue;
					for(int d = 0; d <= 9; ++d){
						if(d == a || d == b || d == c) continue;
						for(int e = 0; e <= 9; ++e){
							if(e == a || e == b || e == c || e == d) continue;
							for(int f = 0; f <= 9; ++f){
								if(f == a || f == b || f == c || f == d || f == e) continue;
								for(int g = 0; g <= 9; ++g){
									if(g == a || g == b || g == c || g == d || g == e || g == f) continue;
									for(int h = 0; h <= 9; ++h){
										if(h == a || h == b || h == c || h == d || h == e || h == f || h == g) continue;
										for(int i = 0; i <= 9; ++i){
											if(i == a || i == b || i == c || i == d || i == e || i == f || i == g || i == h) continue;
											for(int j = 0; j <= 9; ++j){
												if(j == a || j == b || j == c || j == d || j == e || j == f || j == g || j == h || j == i) continue;
												if(Math.abs(a-b) != 1 && Math.abs(a-e) != 1 && Math.abs(a-d) != 1 && Math.abs(a-f) != 1 &&
														Math.abs(b-c) != 1 && Math.abs(f-b) != 1 && Math.abs(e-b) != 1 && Math.abs(g-b) != 1 &&
														Math.abs(f-c) != 1 && Math.abs(g-c) != 1 && 
														Math.abs(d-e) != 1 && Math.abs(d-i) != 1 && Math.abs(d-h) != 1 && 
														Math.abs(e-f) != 1 && Math.abs(e-j) != 1 && Math.abs(e-i) != 1 && Math.abs(e-h) != 1 && 
														Math.abs(f-g) != 1 && Math.abs(f-j) != 1 && Math.abs(f-i) != 1 && 
														Math.abs(g-j) != 1 && 
														Math.abs(h-i) != 1 && Math.abs(i-j) != 1){
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
		System.out.println(count);//1580
	}
}
```


## 剪邮票 （未解决）

> 剪邮票  
如图, 有12张连在一起的12生肖的邮票。  
![图1](/图1.jpg)  
现在你要从中剪下5张来，要求必须是连着的。  
（仅仅连接一个角不算相连）  
比如，图2、图3中，粉红色所示部分就是合格的剪取。  
请你计算，一共有多少种不同的剪取方法。  
![图2](/图2.jpg)  
![图3](/图3.jpg)  

> 请填写表示方案数目的整数。  
注意：你提交的应该是一个整数，不要填写任何多余的内容或说明性文字。

    思路：
    暴力想了好久，本来是想着，先选五个数出来，在通过数字之间的关系判断两两是否相连，但总会有这样那样的问题（很容易变成五个都相连或者每个数都有相连的但连不到一块如{1,2,8,11,12}  
    这道题应该是使用深度遍历，先放一放

``` java
//错误代码
package season7;

public class Seven_cutStamp {

	public static void main(String[] args) {
		// TODO 自动生成的方法存根
		int count = 0;
		for(int a = 1; a <= 12; ++a){
			for(int b = 1; b <= 12; ++b){
				if(b == a) continue;
				for(int c = 1; c <= 12; ++c){
					if(c == a || c == b) continue;
					for(int d = 1; d <= 12; ++d){
						if(d == a || d == b || d == c) continue;
						for(int e = 1; e <= 12; ++e){
							if(e == a || e == b || e == c || e == d) continue;
							
							if(attach(a, b, c, d, e)){
								System.out.println(a +" " + b +" " + c +" " + d +" " + e);
								count++;
							}
						}
					}
				}
			}
		}
		System.out.println(count);//12480
	}

	public static boolean attach(int a, int b, int c, int d, int e){
		int[] id = new int[5];
		id[0] = a;
		id[1] = b;
		id[2] = c; 
		id[3] = d;
		id[4] = e;
		
		boolean flag = true;
		for(int i = 0; i < 5; ++i){
			boolean tempFlag = true;
			for(int j = 0; j < 5; ++j){
				if((Math.abs(id[i]-id[j]) == 1 
						&& ((id[i] != 4 && id[j] != 5) 
						&& (id[i] != 8 && id[j] != 9) 
						&& (id[i] != 5 && id[j] != 4) 
						&& (id[i] != 9 && id[j] != 8)) ) || id[i]+4 == id[j] || id[i]-4 == id[j]){
					
				}else{
					tempFlag = false;
				}
			}
			if(tempFlag == false){
				flag = false;
				break;
			}
		}
			
		return flag;
	}
}

```


## 四平方和

> 四平方和  
四平方和定理，又称为拉格朗日定理：  
每个正整数都可以表示为至多4个正整数的平方和。  
如果把0包括进去，就正好可以表示为4个数的平方和。  
比如：  
5 = 0^2 + 0^2 + 1^2 + 2^2  
7 = 1^2 + 1^2 + 1^2 + 2^2  
（^符号表示乘方的意思）  

> 对于一个给定的正整数，可能存在多种平方和的表示法。  
要求你对4个数排序：  
0 <= a <= b <= c <= d  
并对所有的可能表示法按 a,b,c,d 为联合主键升序排列，最后输出第一个表示法  

> 程序输入为一个正整数N (N<5000000)  
要求输出4个非负整数，按从小到大排序，中间用空格分开  
例如，输入：  
5  
则程序应该输出：  
0 0 1 2  
再例如，输入：  
12  
则程序应该输出：  
0 2 2 2     
再例如，输入：  
773535  
则程序应该输出：  
1 1 267 838  

> 资源约定：  
峰值内存消耗（含虚拟机） < 256M  
CPU消耗  < 3000ms      
请严格按要求输出，不要画蛇添足地打印类似：“请您输入...” 的多余内容。  
所有代码放在同一个源文件中，调试通过后，拷贝提交该源码。
注意：不要使用package语句。不要使用jdk1.7及以上版本的特性。  
注意：主类的名字必须是：Main，否则按无效代码处理。

    思路：
        我的问题：我怎么会从后往前循环各位数寻找（可能因为想着每次砍一平方会快一点？？我这个脑子就不会理性的思考问题吗），问题在于，本题要求输出联合主键最小的，从后往前找就要对各个数进行判断，谁知道我跟这个判断死磕了多久，而且发现需要循环到内层时，肯定会超时（比如773535）
    正常人的脑子：对五个数暴力循环（从0开始），一找到就return，因为是正向循环，第一个找到的肯定是最小的

``` java
//我不太正常的脑子，这个代码看着真的很难受
Scanner scanner = new Scanner(System.in);
int N = scanner.nextInt();
scanner.close();

int i = 0, j = 0, k = 0, l = 0;
int a = Integer.MAX_VALUE, b = Integer.MAX_VALUE, c = Integer.MAX_VALUE, d = Integer.MAX_VALUE;


int count = 5;      //减少循环次数
for(i = (int) Math.sqrt(N); i >= 1; --i){
    int n1 = N-i*i;
    if(n1 == 0){
        count = 1;
        d = i;
        a = 0;b = 0;c = 0;
        break;
    }
    
    if(count >= 2)
    for(j = (int) Math.sqrt(n1); j >= 1; --j){
        int n2 = n1-j*j;
        if(n2 == 0){
            if(a>0 || b>0 || (a==0 && b==0 && j<c) || (a==0 && b==0 && j<=c && i<d)){
                d = i;
                c = j;
                a = 0;b = 0;
            }
            break;
        }
        
        if(count >= 3)
        for(k = (int) Math.sqrt(n2); k >= 1; --k){
            int n3 = n2 - k*k;
            
            if(n3 == 0){
                if(a>0 || (a==0 && k<b) || (a==0 && k<=b && j<c) || (a==0 && k<=b && j<=c&& i<d)){
                    d = i;
                    c = j;
                    b = k;
                    a = 0;
                }
                break;
            }
            
            if(count >= 4)
            for(l = (int) Math.sqrt(n3); l >= 1; --l){
                int n4 = n3 - l*l;
                if(n4 == 0){
                    if(l<a || (l<=a && k<b) || (l<=a && k<=b && j<c) || (l<=a && k<=b && j<=c&& i<d)){
                        d = i;
                        c = j;
                        b = k;
                        a = l;
                    }
                    break;
                }
            }
        }
    }
}

System.out.println(a +" "+ b +" "+ c +" "+ d);
```

``` java
//正常人脑子想的
int s = (new Scanner(System.in)).nextInt();
int a,b,c,d;
for(a=0;a<=Math.sqrt(s);a++) {
    for(b=a;b<=Math.sqrt(s);b++) {
        for(c=b;c<=Math.sqrt(s);c++) {
            for(d=c;d<=Math.sqrt(s);d++) {

                if(s == (Math.pow(a, 2) + Math.pow(b, 2) + Math.pow(c, 2) + Math.pow(d, 2))){
                    System.out.println(a+" "+b+" "+c+" "+d);
                    return;
                }
            }
        }
    }
}
```

## 取球博弈 （未解决）

> 取球博弈  
两个人玩取球的游戏。  
一共有N个球，每人轮流取球，每次可取集合{n1,n2,n3}中的任何一个数目。  
如果无法继续取球，则游戏结束。  
此时，持有奇数个球的一方获胜。  
如果两人都是奇数，则为平局。  
假设双方都采用最聪明的取法，  
第一个取球的人一定能赢吗？  
试编程解决这个问题。  
输入格式：  
第一行3个正整数n1 n2 n3，空格分开，表示每次可取的数目 (0<n1,n2,n3<100)  
第二行5个正整数x1 x2 ... x5，空格分开，表示5局的初始球数(0<xi<1000)  
输出格式：  
一行5个字符，空格分开。分别表示每局先取球的人能否获胜。  
能获胜则输出+，  
次之，如有办法逼平对手，输出0，  
无论如何都会输，则输出-  
例如，输入：  
1 2 3  
1 2 3 4 5  
程序应该输出：  
+ 0 + 0 -  
再例如，输入：  
1 4 5  
10 11 12 13 15  
程序应该输出：  
0 - 0 + +  
再例如，输入：  
2 3 5  
7 8 9 10 11  
程序应该输出：  
+ 0 0 0 0  


> 资源约定：  
峰值内存消耗（含虚拟机） < 256M  
CPU消耗  < 3000ms  
请严格按要求输出，不要画蛇添足地打印类似：“请您输入...” 的多余内容。  
所有代码放在同一个源文件中，调试通过后，拷贝提交该源码。  
注意：不要使用package语句。不要使用jdk1.7及以上版本的特性。  
注意：主类的名字必须是：Main，否则按无效代码处理。  


## 压缩变换 （未解决）
 
> 压缩变换  
小明最近在研究压缩算法。  
他知道，压缩的时候如果能够使得数值很小，就能通过熵编码得到较高的压缩比。  
然而，要使数值很小是一个挑战。  
最近，小明需要压缩一些正整数的序列，这些序列的特点是，后面出现的数字很大可能是刚出现过不久的数字。对于这种特殊的序列，小明准备对序列做一个变换来减小数字的值。  
变换的过程如下：  
从左到右枚举序列，每枚举到一个数字，如果这个数字没有出现过，刚将数字变换成它的相反数，如果数字出现过，则看它在原序列中最后的一次出现后面（且在当前数前面）出现了几种数字，用这个种类数替换原来的数字。  
比如，序列(a1, a2, a3, a4, a5)=(1, 2, 2, 1, 2)在变换过程为：  
a1: 1未出现过，所以a1变为-1；  
a2: 2未出现过，所以a2变为-2；  
a3: 2出现过，最后一次为原序列的a2，在a2后、a3前有0种数字，所以a3变为0；  
a4: 1出现过，最后一次为原序列的a1，在a1后、a4前有1种数字，所以a4变为1；  
a5: 2出现过，最后一次为原序列的a3，在a3后、a5前有1种数字，所以a5变为1。  
现在，给出原序列，请问，按这种变换规则变换后的序列是什么。  
输入格式：  
输入第一行包含一个整数n，表示序列的长度。  
第二行包含n个正整数，表示输入序列。  
输出格式：  
输出一行，包含n个数，表示变换后的序列。  

> 例如，输入：  
5  
1 2 2 1 2  
程序应该输出：  
-1 -2 0 1 1  
再例如，输入：  
12  
1 1 2 3 2 3 1 2 2 2 3 1  
程序应该输出：  
-1 0 -2 -3 1 1 2 2 0 0 2 2  
数据规模与约定  
对于30%的数据，n<=1000；  
对于50%的数据，n<=30000；  
对于100%的数据，1 <=n<=100000，1<=ai<=10^9  




资源约定：
峰值内存消耗（含虚拟机） < 256M
CPU消耗  < 3000ms


请严格按要求输出，不要画蛇添足地打印类似：“请您输入...” 的多余内容。

所有代码放在同一个源文件中，调试通过后，拷贝提交该源码。
注意：不要使用package语句。不要使用jdk1.7及以上版本的特性。
注意：主类的名字必须是：Main，否则按无效代码处理。

