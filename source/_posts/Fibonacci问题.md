---
title: Fibonacci问题
date: 2019-03-11 14:44:27
tags:
    - DynamicProblem
    - Recursion
categories:  
    - 算法
description: 由Fibonacci体会动态规划
---


### 由Fibonacci体会动态规划

1. #### Recursion  
    ``` java
    public static int fib(int n){
        if(n == 1 || n == 2){
            return 1;
        }
        
        return fib(n-1) + fib(n-2);
	}
    ```
2. #### top - down  
    + 保存递归结果，减少冗余递归

    ``` java
    //注意递归树
	public static int fibonacci(int n){
		int[] temp = new int[n+1];

		for(int i = 0; i < temp.length; ++i){
			temp[i] = -1;
		}
		
		return fib(n, temp);
	}
	
	public static int fib(int n, int[] temp){
		if(n == 1 || n == 2){
			return 1;
		}
		
		if(temp[n] != -1){
			return temp[n];
		}
		
		int fib = fib(n-1, temp) + fib(n-2, temp);
		
		temp[n] = fib;
		
		return fib;
	 }
    ```

3. #### DP

    ``` java
    public static int fib1(int n){
		int[] temp = new int[n+1];
		
		temp[0] = 0;		//从第0项算起
		temp[1] = 1;
		
		for(int i = 2; i < temp.length; ++i){
			temp[i] = temp[i-1] + temp[i-2];
		}
			
		return temp[n];
	}  
    
    ```  
    + 可以发现，我们需要的只是第n项的结果，不需要保存之前的值，所以还可以对空间进行优化  

    ``` java
    public static int fib2(int n){
		if(n <= 0){
			return n;
		}
		int temp1 = 0;
		int temp2 = 1;

		int tempn = 1;
		
		for(int i = 2; i <= n; ++i){
			tempn = temp1 + temp2;
			temp1 = temp2;
			temp2 = tempn;
		}
		
		return tempn;
	}
    ```