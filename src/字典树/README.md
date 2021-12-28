# 字典树

什么是字典树？字典树也就是前缀树，字典树就是一个树形结构。该树是一个棵26叉树，因为每一个结点都是表示的是，当前结点的字符的下一个字符，树的深度优先遍历的从根到叶子的一条路径就是一个单词。这样的话，其实不是不难想象，前缀相同的树在字典树中是有相同的路径的。

## 实现字典树

根据定义，字典树的最小实现所需要的属性有两个，其中一个是判断结点是不是单词结尾的isEnd，另外一个属性就是当前结点的孩子结点，孩子可能是26个英文字母的随机一个，假设所有单词都是由小写字母组成，所以当前结点的孩子存储就是一个长度为26的数组。

主要实现的功能就是插入，查询前缀，查询单词，查询是否以某个特定前缀开始的字符串

```java
package com.lxl.java.model;

import java.util.Arrays;

/**
 * @author LiXianLei
 * @time 2021/12/28 01:15
 */
public class Trie {
    private boolean isEnd;
    private Trie[] children;

    public Trie(){
        isEnd = false;
        children = new Trie[26];
    }
    /**
     * @author LiXianLei
     * @describtion //TODO 向字典树中插入单词
     * @return {@null}
     * @param word
     * @time 2021/12/28 1:27
     **/
    public void insert(String word){
        if(word.length() == 0)return;
        Trie node = this;
        char[] cs = word.toCharArray();
        for(char c : cs){
            int idx = c - 'a';
            if(node.children[idx] == null){
                node.children[idx] = new Trie();
            }
            node = node.children[idx];
        }
        node.isEnd = true;
    }

    /**
     * @author LiXianLei
     * @describtion //TODO 搜索前缀
     * @return {@link Trie}
     * @param prefix
     * @time 2021/12/28 1:28
     **/
    public Trie searchPrefix(String prefix){
        if(prefix.length() == 0)return null;
        Trie node = this;
        char[] cs = prefix.toCharArray();
        for(char c : cs){
            node = node.children[c - 'a'];
            if(node == null)return null;
        }
        return node;
    }

    /**
     * @author LiXianLei
     * @describtion //TODO 单词是否与指定字符串为起始的字符串
     * @return {@link boolean}
     * @param prefix->String
     * @time 2021/12/28 1:29
     **/
    public boolean startWith(String prefix){
        return searchPrefix(prefix) != null;
    }

    /**
     * @author LiXianLei
     * @describtion //TODO 搜索单词是否存在于字典树
     * @return {@link boolean}
     * @param word->String
     * @time 2021/12/28 1:30
     **/
    public boolean search(String word){
        Trie node = searchPrefix(word);
        return node != null && node.isEnd;
    }

    public boolean isEnd() {
        return isEnd;
    }

    public void setEnd(boolean end) {
        isEnd = end;
    }

    public Trie[] getChildren() {
        return children;
    }

    public void setChildren(Trie[] children) {
        this.children = children;
    }
}

```

力扣中有实现字典树的题目[208. 实现 Trie (前缀树) - 力扣（LeetCode） (leetcode-cn.com)](https://leetcode-cn.com/problems/implement-trie-prefix-tree/)

![实现前缀树](https://gitee.com/QingShanxl/pictures/raw/master/img//image-20211228111808668.png)