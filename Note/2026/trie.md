# 字典树（前缀 树）

## 什么是Trie

[字典树](https://zhuanlan.zhihu.com/p/675482843)

一种对于字符串的数据结构

能够将查询字典中的单词的时间复杂度降低到$O(W)$（$W$代表单词的长度）

![img](images/v2-ac14f9a2ec7cbe2c46247542f6df8bc5_1440w.jpg)

每个节点有若干个指向下一个节点的指针

向下兼容：每个节点添加一个标识符，判断该节点是否是某个单词的结尾某一个单词的结尾只靠叶子节点是不能区别出来的，因此我们在设计Node节点是，应该添加一个IsWord，判断节点上是否是单词的结尾

## Trie的实现

### 节点类（Node）

```java
//设计节点类
private class Node{
    //判断是否是一个单词        
    public boolean isWord;
    //每个节点有若干个指向下个节点的指针
            public TreeMap<Character,Node> next;
	//有参构造：对该节点进行初始化
            public Node (boolean isWord){
                this.isWord=isWord;
                next = new TreeMap<>();
            }
	//无参构造：默认当前节点不是单词的结尾
            public Node(){
                this(false);
            }
}
```

### Trie的实现

```java
public class Trie{
            private class Node{
            public boolean isWord;
            public TreeMap<Character,Node> next;

            public Node (boolean isWord){
                this.isWord=isWord;
                next = new TreeMap<>();
            }

            public Node(){
                this(false);
            }
            }
            private Node root;
            private int size;

            public Trie(){
                root = new Node();
                size = 0;
            }
			//获取trie中存储单词的数量
            public int getSize(){
                return size;
            }
        }
```

### 添加元素

```java
public void add(String word){
                Node cur = root;
                for(int i = 0; i < word.length();i++){
                    //将这个单词拆成一个一个字符
                    char c = word.charAt(i);
                    //如果当前节点的若干个子节点，没有存储当前字符的节点，则需要创建一个子节点，存储当前字符
                    if(cur.next,get(c) == null){
                        cur.next.put(c.new Node ());
                    }
                    cur = cur.next.get(c);
        
                }
    		   //对添加的新单词遍历结束后，判断当前节点是否为单词的结尾，如果不是我们才对size加一
                if(!cur.isWord){
                    cur.isWord = true;
                    size ++;
                }
            }
```

### 查询操作

```java
public boolean contains(String word){
                Node cur = root;
                for(int i = 0; i < word.length(); i++){
                    char c = word.charAt(i);
                    if(cur.next.get(c) == null){
                        return false;
                    }
                    cur = cur.next.get(c);
                }
                return cur.isWord;
            }
```

与查询类型，我们可以写一个是否以某个单词为前缀的单词

```java
public boolean isPrefix (String prefix){
                Node cur = root;
                for(int i = 0; i < prefix.length(); i++){
                    char c =  prefix.charAt(i);
                    if(cur.next.get(c) == null) return false;
                    cur = cur.next.get(c);
                }
                return true;
            }
```

