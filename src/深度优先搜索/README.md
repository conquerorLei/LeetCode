# 深度优先搜索

深度优先搜索(<font color='red'>Depth-First-Search</font>， 简称DFS)是一种遍历树或者图的方法。

他的核心思想就是从一个点v出发，一直沿着某一条路出发，直到在路的结尾还有没有达到目标解，那么就返回上一个有分岔路口的结点，换一条路再一直走到底。

> 最底层的思想就是<font color='lawngreen'>不撞南墙不回头，就算撞了南墙，回头换了路接着撞</font>

深度优先搜索的基本特征就是，<font color='orange'>遍历所有的元素</font>

深度优先搜索的数据结构是栈。

深度优先搜索有两个注意事项：

- 回溯(能够完成所有元素搜索的基础条件)
- 剪枝(去重)

### 带回溯的深度优先搜索

**题目**：给定一个整数n，输出$[1, n]$的全排列

**例题**：

输入实例

```java
n = 3;
```

输出示例:

```java
[[1, 2, 3], [1, 3, 2], [2, 1, 3], [2, 3, 1], [3, 1, 2], [3, 2, 1]]
```

代码：

```java
package com.lxl.java.solution;

import java.util.LinkedList;
import java.util.List;
import java.util.Scanner;

/**
 * @author LiXianLei
 * @time 2021/12/15 15:29
 */
public class PermuteI {
    private int n;
    private int[] state;
    private boolean[] used;
    private List<Integer> temp;
    private List<List<Integer>> res = new LinkedList<>();

    public PermuteI(int n){
        this.n = n;
        state = new int[n];
        used = new boolean[n];
    }

    public void dfs(int u){
        if(u >= n){
            temp = new LinkedList<>();
            for(int i : state){
                temp.add(i);
            }
            res.add(temp);
            return;
        }
        for(int i = 1; i <= n; i++){
            if(!used[i - 1]){
                state[u] = i;
                used[i - 1] = true;
                dfs(u + 1);
                state[u] = 0;
                used[i - 1] = false;
            }
        }
    }

    public List<List<Integer>> getRes() {
        return res;
    }

    public static void main(String[] args) {
        Scanner scan = new Scanner(System.in);
        int n = scan.nextInt();
        PermuteI pi = new PermuteI(n);
        pi.dfs(0);
        System.out.println(pi.getRes());
    }
}
```

