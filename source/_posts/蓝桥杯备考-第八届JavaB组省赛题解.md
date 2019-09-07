---
title: 蓝桥杯备考-第八届JavaB组省赛题解
date: 2019-03-21 18:27:06
tags:
categories: 
    - 蓝桥杯

description: 第八届JavaB组省赛题解
---

## 购物单
 
> 标题： 购物单  
小明刚刚找到工作，老板人很好，只是老板夫人很爱购物。老板忙的时候经常让小明帮忙到商场代为购物。小明很厌烦，但又不好推辞。  
这不，XX大促销又来了！老板夫人开出了长长的购物单，都是有打折优惠的。  
小明也有个怪癖，不到万不得已，从不刷卡，直接现金搞定。  
现在小明很心烦，请你帮他计算一下，需要从取款机上取多少现金，才能搞定这次购物。  
取款机只能提供100元面额的纸币。小明想尽可能少取些现金，够用就行了。  
你的任务是计算出，小明最少需要取多少现金。  
以下是让人头疼的购物单，为了保护隐私，物品名称被隐藏了。

<pre>
****     180.90       88
****      10.25       65
****      56.14        9
****     104.65        9
****     100.30       88
****     297.15        50
****      26.75       65
****     130.62        50
****     240.28       58
****     270.62        8
****     115.87       88
****     247.34       95
****      73.21        9
****     101.00        50
****      79.54        50
****     278.44        7
****     199.26        50
****      12.97        9
****     166.30       78
****     125.50       58
****      84.98        9
****     113.35       68
****     166.57        50
****      42.56        9
****      81.90       95
****     131.78        8
****     255.89       78
****     109.17        9
****     146.69       68
****     139.33       65
****     141.16       78
****     154.74        8
****      59.42        8
****      85.44       68
****     293.70       88
****     261.79       65
****      11.30       88
****     268.27       58
****     128.29       88
****     251.03        8
****     208.39       75
****     128.88       75
****      62.06        9
****     225.87       75
****      12.89       75
****      34.28       75
****      62.16       58
****     129.12        50
****     218.37        50
****     289.69        8
</pre>

> 需要说明的是，88折指的是按标价的88%计算，而8折是按80%计算，余者类推。  
特别地，半价是按50%计算。  
请提交小明要从取款机上提取的金额，单位是元。  
答案是一个整数，类似4300的样子，结尾必然是00，不要填写任何多余的内容。  
特别提醒：不许携带计算器入场，也不能打开手机。  

    该题手动输入计算器也比较麻烦，对给出的数据做一个整理  
    将半价改成5， 删去折字  
    然后考虑怎样读入文本，一行一行的读取（复制进EXCEL里可以知道有多少行），按多个空格split("\\s+"), 取数组后两个数据
    正则表达式挺有用的  

``` java
Scanner scanner = new Scanner(System.in);
int N = 50;
float[][] count = new float[N][2];

String[] str = new String[3];
for(int i = 0; i < N; ++i){
    str = scanner.nextLine().split("\\s+");
    for(int j = 0; j < 2; ++j){
        count[i][j] = Float.valueOf(str[j+1]);
    }
}

for(int i = 0; i < N; ++i){
    System.out.println(Arrays.toString(count[i]));
}

float result = 0;
for(int i = 0; i < N; ++i){
    if(count[i][1] < 10){
        result += count[i][0] * count[i][1]/10;
    }else{
        result += count[i][0] * count[i][1]/100;
    }
}
System.out.println(result);//5136.8594
//5200
```

## 纸牌三角形（暴力）

> 标题：纸牌三角形  
A,2,3,4,5,6,7,8,9 共9张纸牌排成一个正三角形（A按1计算）。要求每个边的和相等。    
下图就是一种排法（如有对齐问题，参看p1.png）。  

<pre>
      A
     9 6
    4   8
   3 7 5 2
</pre>

> 这样的排法可能会有很多。   
如果考虑旋转、镜像后相同的算同一种，一共有多少种不同的排法呢？  
请你计算并提交该数字。  
注意：需要提交的是一个整数，不要提交任何多余内容。 

    思路：我的猪脑壳没有想出来；这种题就不要找规律了好伐，考虑怎样使用代码模拟
    别人的脑壳：暴力模拟，循环生成9个不同的数(1-9)，使用边相等条件进行判断  
    考虑镜像和旋转，一种情况有三种镜像，三种旋转，所以将循环结果/6即可

``` java
int sum = 0;
for(int a = 1; a <= 9; ++a){
    for(int b = 1; b <= 9; ++b){
        for(int c = 1; c <= 9; ++c){
            for(int d = 1; d <= 9; ++d){
                for(int e = 1; e <= 9; ++e){
                    for(int f = 1; f <= 9; ++f){
                        for(int g = 1; g <= 9; ++g){
                            for(int h = 1; h <= 9; ++h){
                                for(int i = 1; i <= 9; ++i){
                                    
                                    if(a+b+c+d == d+e+f+g && a+i+h+g == d+e+f+g){
                                        if(a!=b && a!=c && a!=d && a!=e && a!=f && a!=g && a!=h && a!=i){
                                            if(b!=c && b!=d && b!=e && b!=f && b!=g && b!=h &&b!=i){
                                                if(c!=d && c!=e && c!=f && c!=g && c!=h && c!=i){
                                                    if(d!=e && d!=f && d!=g && d!=h && d!=i){
                                                        if(e!=f && e!=g && e!=h && e!=i){
                                                            if(f!=g && f!=h && f!=i){
                                                                if(g!=h && g!=i){
                                                                    if(h!=i){
                                                                        sum++;
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
System.out.println(sum/6);//144
```

## 承压计算

> 标题：承压计算  
X星球的高科技实验室中整齐地堆放着某批珍贵金属原料。  
每块金属原料的外形、尺寸完全一致，但重量不同。  
金属材料被严格地堆放成金字塔形。  

<pre>
                             7 
                            5 8 
                           7 8 8 
                          9 2 7 2 
                         8 1 4 9 1 
                        8 1 8 8 4 1 
                       7 9 6 1 4 5 4 
                      5 6 5 5 6 9 5 6 
                     5 5 4 7 9 3 5 5 1 
                    7 5 7 9 7 4 7 3 3 1 
                   4 6 4 5 5 8 8 3 2 4 3 
                  1 1 3 3 1 6 6 5 5 4 4 2 
                 9 9 9 2 1 9 1 9 2 9 5 7 9 
                4 3 3 7 7 9 3 6 1 3 8 8 3 7 
               3 6 8 1 5 3 9 5 8 3 8 1 8 3 3 
              8 3 2 3 3 5 5 8 5 4 2 8 6 7 6 9 
             8 1 8 1 8 4 6 2 2 1 7 9 4 2 3 3 4 
            2 8 4 2 2 9 9 2 8 3 4 9 6 3 9 4 6 9 
           7 9 7 4 9 7 6 6 2 8 9 4 1 8 1 7 2 1 6 
          9 2 8 6 4 2 7 9 5 4 1 2 5 1 7 3 9 8 3 3 
         5 2 1 6 7 9 3 2 8 9 5 5 6 6 6 2 1 8 7 9 9 
        6 7 1 8 8 7 5 3 6 5 4 7 3 4 6 7 8 1 3 2 7 4 
       2 2 6 3 5 3 4 9 2 4 5 7 6 6 3 2 7 2 4 8 5 5 4 
      7 4 4 5 8 3 3 8 1 8 6 3 2 1 6 2 6 4 6 3 8 2 9 6 
     1 2 4 1 3 3 5 3 4 9 6 3 8 6 5 9 1 5 3 2 6 8 8 5 3 
    2 2 7 9 3 3 2 8 6 9 8 4 4 9 5 8 2 6 3 4 8 4 9 3 8 8 
   7 7 7 9 7 5 2 7 9 2 5 1 9 2 6 5 3 9 3 5 7 3 5 4 2 8 9 
  7 7 6 6 8 7 5 5 8 2 4 7 7 4 7 2 6 9 2 1 8 2 9 8 5 7 3 6 
 5 9 4 5 5 7 5 5 6 3 5 3 9 5 8 9 5 4 1 2 6 1 4 3 5 3 2 4 1 
X X X X X X X X X X X X X X X X X X X X X X X X X X X X X X 
</pre>
  

> 其中的数字代表金属块的重量（计量单位较大）。  
最下一层的X代表30台极高精度的电子秤。  
假设每块原料的重量都十分精确地平均落在下方的两个金属块上，  
最后，所有的金属块的重量都严格精确地平分落在最底层的电子秤上。  
电子秤的计量单位很小，所以显示的数字很大。  
工作人员发现，其中读数最小的电子秤的示数为：2086458231  
请你推算出：读数最大的电子秤的示数为多少？  
注意：需要提交的是一个整数，不要填写任何多余的内容。  

    我的思路：我的脑子还是有思路的，使用另一个数组存放各行各列重量，[i, j]等于上一层[i-1, j-1]/2+[i-1][j]/2再加上当前层金属块重量    
    （边界单独判断就是了）（记住数组初始化后默认赋值为0）
    不必考虑金字塔形状，反正往左对齐位置关系都不变就完事儿了  
    重点：1. 单位不是1，需要根据最小示数推算单位   
        2. 因为涉及到除法，考虑数值精度，一开始使用float类型发现结果不对，是小数

``` java
Scanner scanner = new Scanner(System.in);
double[][] dp = new double[30][30];

double[][] arr = new double[30][30];
for(int i = 0; i < 29; ++i){
    String[] temp = scanner.nextLine().trim().split(" ");
    for(int j = 0; j < temp.length; ++j){
        arr[i][j] = Float.valueOf((temp[j]));
    }
}

dp[0][0] = arr[0][0];
for(int i = 1; i < 30; ++i){
    for(int j = 0 ; j < 30; ++j){
        //(i-1, j-1) (i-1, j)
        dp[i][j] = arr[i][j];   
        if(j - 1 >= 0){ //边界
            dp[i][j] += dp[i-1][j-1]/2; 
        }
        dp[i][j] += dp[i-1][j]/2; 
    }
}

double max = Double.MIN_VALUE;
double min = Double.MAX_VALUE;
for(int i = 0; i < 30; ++i){
    if(dp[29][i] > max){
        max = dp[29][i];
    }
    if(dp[29][i] < min){
        min = dp[29][i];
    }
}
System.out.println(2086458231/min);
System.out.println(max);
System.out.println(2086458231/min*max);

//7.2665192664E10 = 72665192664
```

## 魔方状态（未解决）

> 标题：魔方状态  
二阶魔方就是只有2层的魔方，只由8个小块组成。  
如图p1.png所示。  
![魔方](/p1.png)
小明很淘气，他只喜欢3种颜色，所有把家里的二阶魔方重新涂了颜色，如下：  
前面：橙色  
右面：绿色  
上面：黄色  
左面：绿色  
下面：橙色  
后面：黄色  
请你计算一下，这样的魔方被打乱后，一共有多少种不同的状态。  
如果两个状态经过魔方的整体旋转后，各个面的颜色都一致，则认为是同一状态。  
请提交表示状态数的整数，不要填写任何多余内容或说明文字。  

## 取位数

> 标题：取数位
求1个整数的第k位数字有很多种方法。
以下的方法就是一种。
``` java
public class Main
{
	static int len(int x){
		if(x<10) return 1;
		return len(x/10)+1;
	}
	
	// 取x的第k位数字
	static int f(int x, int k){
		if(len(x)-k==0) return x%10;
		return ______________________;  //填空
	}
	
	public static void main(String[] args)
	{
		int x = 23513;
		//System.out.println(len(x));
		System.out.println(f(x,3));
	}
}
```

> 对于题目中的测试数据，应该打印5。  
请仔细分析源码，并补充划线部分所缺少的代码。  
注意：只提交缺失的代码，不要填写任何已有内容或说明性的文字。  

    思路：这道题太坑了，我为了证明他说的第k位是从左起的还是从右起的用了好久  
    按常理应该是从最小位算第一位啊，而且从左起的话代码简单到我怀疑自己  
    可是看网上大家的答案，好像只有我一个人有这个问题，姑且认为他从左起的吧  
    代码很简单，就是一个简单的递归，/10，使数值长度等于要取的位数K时返回对10取余的值（即此时的最低位）

``` java
return f(x/10, k);  //填空
```

## 最大公共子串

> 标题：最大公共子串  
最大公共子串长度问题就是：  
求两个串的所有子串中能够匹配上的最大长度是多少。   
比如："abcdkkk" 和 "baabcdadabc"，  
可以找到的最长的公共子串是"abcd",所以最大公共子串长度为4。  
下面的程序是采用矩阵法进行求解的，这对串的规模不大的情况还是比较有效的解法。  
请分析该解法的思路，并补全划线部分缺失的代码。  

``` java
public class Main
{
	static int f(String s1, String s2)
	{
		char[] c1 = s1.toCharArray();
		char[] c2 = s2.toCharArray();
		
		int[][] a = new int[c1.length+1][c2.length+1];
		
		int max = 0;
		for(int i=1; i<a.length; i++){
			for(int j=1; j<a[i].length; j++){
				if(c1[i-1]==c2[j-1]) {
					a[i][j] = __________________;  //填空 
					if(a[i][j] > max) max = a[i][j];
				}
			}
		}
		
		return max;
	}
	
	public static void main(String[] args){
		int n = f("abcdkkk", "baabcdadabc");
		System.out.println(n);
	}
}
```

> 注意：只提交缺少的代码，不要提交已有的代码和符号。也不要提交说明性文字。

    思路：很奇妙的代码，感觉自己永远也想不到要这样做  
    但是仔细分析以下还是能够懂， 画个图  
    理清他构造的a二维数组存的是什么，行和列分别是什么，就很好懂  
    行和列分别代表对应串，然后比如将s1的当前字母分别和s2的各个字母比较，如果相同  
    我们可以知道，如果两个串有对应相同的长度大于等于2的子串时，一定可以在二维数组上连成一条斜线  
    且因为构造的a二维数组比原字符串长一个单位，用在第一行和第一列，这时候默认值是0对于理解这个就显得很重要  

``` java
a[i][j] = a[i-1][j-1]+1; //填空 
```

## 日期问题

> 标题：日期问题   
小明正在整理一批历史文献。这些历史文献中出现了很多日期。小明知道这些日期都在1960年1月1日至2059年12月31日。  
令小明头疼的是，这些日期采用的格式非常不统一，有采用年/月/日的，有采用月/日/年的，还有采用日/月/年的。  
更加麻烦的是，年份也都省略了前两位，使得文献上的一个日期，存在很多可能的日期与其对应。    
比如02/03/04，可能是2002年03月04日、2004年02月03日或2004年03月02日。    
给出一个文献上的日期，你能帮助小明判断有哪些可能的日期对其对应吗？  

> 输入  
一个日期，格式是"AA/BB/CC"。  (0 <= A, B, C <= 9)    
输入  
输出若干个不相同的日期，每个日期一行，格式是"yyyy-MM-dd"。多个日期按从早到晚排列。    
样例输入  
02/03/04    
样例输出  
2002-03-04    
2004-02-03    
2004-03-02   
资源约定：  
峰值内存消耗（含虚拟机） < 256M  
CPU消耗  < 1000ms  

    思路：思路还是很简单的
    说一下要注意的细节，写半天了才发现题没看清  
    日期格式只有“年/月/日，月/日/年，日/月/年”  
    对二月、闰年等需要单独判断
    难点：要求从小到大输出 - 将年月日乘以对应比列形成一个整数，在对该整数数组进行排序，还原输出
    总觉得自己思路很乱，代码更乱

``` java
package season8;

import java.util.Arrays;
import java.util.Scanner;

/*
 * 从小到大输出？？
 */

public class Seven_PossibleTime {

	public static void main(String[] args) {
		// TODO 自动生成的方法存根
		Scanner scanner = new Scanner(System.in);
		
		String[] temp = scanner.nextLine().split("/");
		int[] time = new int[3];
		for(int i = 0 ; i< 3; ++i){
			time[i] = Integer.valueOf(temp[i]);
		}
		
		int[] z = new int[3];
		int count = 0;
		
		int year = 0;
		int month = 0;
		int day = 0;
		if(canBeYear(time[0])){
			year = time[0];
			if(canBeMonth(time[1])){
				month = time[1];
				if(canBeDay(year, month, time[2])){
					day = time[2];
					//System.out.println(createYear(year) + "-" + createMonth(month) + "-" + createDay(day));
					z[count++] = createYear(year)*10000+month*100+day;
				}
			}
			
		}
		if(canBeYear(time[2])){
			year = time[2];
			if(canBeMonth(time[0])){
				month = time[0];
				if(canBeDay(year, month, time[1])){
					day = time[1];
					//System.out.println(createYear(year) + "-" + createMonth(month) + "-" + createDay(day));
					z[count++] = createYear(year)*10000+month*100+day;
				}
			}
			
			if(canBeMonth(time[1])){
				month = time[1];
				if(canBeDay(year, month, time[0])){
					day = time[0];
					//System.out.println(createYear(year) + "-" + createMonth(month) + "-" + createDay(day));
					z[count++] = createYear(year)*10000+month*100+day;
				}
			}
		}
		
		Arrays.sort(z);
		for(int i = 0; i < count; ++i){
			int y = z[i]/10000;
			int m = z[i]/100%100;
			int d = z[i]%100;
			System.out.println(y + "-" + createMonth(m) + "-" + createDay(d));
			
		}
		
	}
	
	public static int createYear(int y){
		if(y <= 59){
			return  y + 2000;
		}else{
			return y + 1900;
		}
	}
	
	public static String createMonth(int m){
		if(m < 10){
			return "0"+m;
		}else{
			return Integer.toString(m);
		}
	}
	
	public static String createDay(int d){
		if(d < 10){
			return "0"+d;
		}else{
			return Integer.toString(d);
		}
	}
	
	public static boolean canBeYear(int y){
		if(y <= 60){
			return true;
		}else{
			return false;
		}
	}
	
	public static boolean canBeMonth(int m){
		if(m <= 12 && m >= 1){
			return true;
		}else{
			return false;
		}
	}
	
	public static boolean canBeDay(int y, int m, int d){
		if(d >= 32 || d <= 0){
			return false;
		}
		
		if(m == 2){
			if(d > 29){
				return false;
			}
			if(d == 29){
				if(!ifLeapYear(y)){
					return false;
				}
			}
		}
		
		if(!ifBigMonth(m)){
			if(d == 31){
				return false;
			}
		}
		
		return true;
	}
	
	
	//闰年二月有29号，非闰年二月只到28号
	public static boolean ifLeapYear(int y){
		if(y <= 59){
			y += 2000;
		}else{
			y += 1900;
		}
		
		if(y % 400 == 0 || (y % 4 == 0 && y % 100 != 0)){
			return true;
		}else{
			return false;
		}
	}
	
	public static boolean ifBigMonth(int m){
		if(m == 1 || m == 3 || m == 5 || m == 7 || m == 8 || m == 10 || m == 12){
			return true;
		}else{
			return false;
		}
	}
	
}

```

## 包子凑数（未解决）

> 标题：包子凑数
小明几乎每天早晨都会在一家包子铺吃早餐。他发现这家包子铺有N种蒸笼，其中第i种蒸笼恰好能放Ai个包子。  
每种蒸笼都有非常多笼，可以认为是无限笼。  
每当有顾客想买X个包子，卖包子的大叔就会迅速选出若干笼包子来，使得这若干笼中恰好一共有X个包子。  
比如一共有3种蒸笼，分别能放3、4和5个包子。当顾客想买11个包子时，大叔就会选2笼3个的再加1笼5个的（也可能选出1笼3个的再加2笼4个的）。  
当然有时包子大叔无论如何也凑不出顾客想买的数量。比如一共有3种蒸笼，分别能放4、5和6个包子。而顾客想买7个包子时，大叔就凑不出来了。  
小明想知道一共有多少种数目是包子大叔凑不出来的。  

> 输入
第一行包含一个整数N。(1 <= N <= 100)  
以下N行每行包含一个整数Ai。(1 <= Ai <= 100)    
输出  
一个整数代表答案。如果凑不出的数目有无限多个，输出INF。  

> 例如，  
输入：  
2    
4    
5     
程序应该输出：  
6  

> 再例如，  
输入：   
2  
4  
6    
程序应该输出：  
INF  
样例解释：  
对于样例1，凑不出的数目包括：1, 2, 3, 6, 7, 11。    
对于样例2，所有奇数都凑不出来，所以有无限多个。  

## 分巧克力

> 标题： 分巧克力  
儿童节那天有K位小朋友到小明家做客。小明拿出了珍藏的巧克力招待小朋友们。  
小明一共有N块巧克力，其中第i块是Hi x Wi的方格组成的长方形。  
为了公平起见，小明需要从这 N 块巧克力中切出K块巧克力分给小朋友们。切出的巧克力需要满足：  
    1. 形状是正方形，边长是整数    
    2. 大小相同   
例如一块6x5的巧克力可以切出6块2x2的巧克力或者2块3x3的巧克力。  
当然小朋友们都希望得到的巧克力尽可能大，你能帮小Hi计算出最大的边长是多少么？  

> 输入  
第一行包含两个整数N和K。(1 <= N, K <= 100000)    
以下N行每行包含两个整数Hi和Wi。(1 <= Hi, Wi <= 100000)  
输入保证每位小朋友至少能获得一块1x1的巧克力。     
输出  
输出切出的正方形巧克力最大可能的边长。

> 样例输入：  
2 10  
6 5  
5 6  
样例输出：  
2


    思路：因为需要输出尽可能大，所以从最大边长往回循环  
    循环每个边长，计算该边长能分多少块巧克力，第一个大于可分块数大于等于小朋友人数的边长为所求

``` java
import java.util.Scanner;

public class Nine_DivedChoclate {

	public static void main(String[] args) {
		// TODO 自动生成的方法存根
		Scanner scanner = new Scanner(System.in);
		int N = scanner.nextInt();
		int K = scanner.nextInt();
		int[][] cho = new int[N][2];
		
		int maxSide = Integer.MIN_VALUE;
		int result = 0;
		
		for(int i = 0; i < N; ++i){
			for(int j = 0; j < 2; ++j){
				cho[i][j] = scanner.nextInt();
				if(cho[i][j] > maxSide){
					maxSide = cho[i][j];
				}
			}
		}
		
		for(int k = maxSide; k > 0; --k){	//切分边长
			int tempK = 0;
			for(int i = 0; i < N; ++i){
				int height = cho[i][0];
				int width = cho[i][1];
				tempK += singleDivide(width, height, k);
			}
			
			if(tempK >= K){
				result = k;
				break;
			}
		}
		
		System.out.println(result);
		
	}
	
	public static int singleDivide(int width, int height, int L){
		if(width < L || height < L){
			return 0;
		}
		
		return (height/L)*(width/L);
	}
}

```

## k倍区间（未解决）

> 标题： k倍区间  
给定一个长度为N的数列，A1, A2, ... AN，  
如果其中一段连续的子序列Ai, Ai+1, ... Aj(i <= j)之和是K的倍数，  
我们就称这个区间[i, j]是K倍区间。    
你能求出数列中总共有多少个K倍区间吗？    

> 输入  
第一行包含两个整数N和K。(1 <= N, K <= 100000)   
以下N行每行包含一个整数Ai。(1 <= Ai <= 100000)   
输出  
输出一个整数，代表K倍区间的数目。    
例如，  
输入：  
5 2  
1    
2  
3  
4  
5  
程序应该输出：  
6  


