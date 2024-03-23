# AcWing 算法基础课 -- 动态规划

## AcWing 902. 最短编辑距离

`难度：简单`

### 题目描述

给定两个字符串A和B，现在要将A经过若干操作变为B，可进行的操作有：

1. 删除–将字符串A中的某个字符删除。
2. 插入–在字符串A的某个位置插入某个字符。
3. 替换–将字符串A中的某个字符替换为另一个字符。

现在请你求出，将A变为B至少需要进行多少次操作。

**输入格式**

第一行包含整数n，表示字符串A的长度。

第二行包含一个长度为n的字符串A。

第三行包含整数m，表示字符串B的长度。

第四行包含一个长度为m的字符串B。

字符串中均只包含大写字母。

**输出格式**

输出一个整数，表示最少操作次数。

**数据范围**

1≤n,m≤1000

```r
输入样例：

10 
AGTCTGACGC
11 
AGTAAGTAGGC

输出样例：

4
```

### Solution

```java
/**
 * dp数组的定义：dp[i][j]表示以i - 1结尾的串s1,变为以j - 1结尾的串s2所需要的最少操作次数.dp[s1.length()][s2.length()];
 * 递推公式：
 * if(s1.charAt(i - 1) == s2.charAt(j - 1)){
 dp[i][j] = dp[i - 1][j - 1];
 }else{
 dp[i][j] = Math.min(Math.min(dp[i - 1][j], dp[i][j - 1]), dp[i - 1][j - 1]) + 1;
 }
 * 初始化：
 *   dp[0][j] = j;
 *   dp[i][0] = i;
 */

import java.io.*;
import java.util.*;

public class Main{
    static final int N = 1010;
    static int[][] dp = new int[N][N];
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int m = sc.nextInt();
        String s1 = sc.next();
        int n = sc.nextInt();
        String s2 = sc.next();

        //注意m和n的边界也要初始化！
        for(int i = 0; i <= m; i ++) dp[i][0] = i;
        for(int j = 0; j <= n; j ++) dp[0][j] = j;

        for(int i = 1; i <= m; i ++){
            for(int j = 1; j <= n; j ++){
                if(s1.charAt(i - 1) == s2.charAt(j - 1)){
                    dp[i][j] = dp[i - 1][j - 1];
                }else{
                    dp[i][j] = Math.min(Math.min(dp[i - 1][j], dp[i][j - 1]), dp[i - 1][j - 1]) + 1;
                }
            }
        }
        System.out.println(dp[m][n]);
    }
}
```