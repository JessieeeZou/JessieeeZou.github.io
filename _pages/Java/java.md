---
title: Java Notes
author: Xiaoxu Zou
date: 2022-03-31
category: Java
layout: page
---

1. 可以直接根据函数返回的参数创建新的所需的数组或其他东西
   char定义时用单引号，只能有一个字母，数字。 char c ='c'; 而String用双引号，可以是一个，也可能是多个字母，汉字等。 就是所谓的字符串。
2. String相关：(string s) --- string要按字符遍历需要先转换成Array用函数s.toCharArray()，最后再转换成string用函数s.toString()
- Java中string是不可变的，因此要初始化一个StringBuilder。
```java
s.length();
s.charAt(i);
for (int i = 0; i < s.length(); i++); 
//可以改写成for (char c : s.toCharArray());
StringBuilder res = new StringBuilder();
res.append(c);
res.toString();
s1.equals(s2);
//字符串的比较不能用==，而是用equals方法
```
3. HashMap:
```java
HashMap<Character, Integer> map = new HashMap<>();
hashmap.getOrDefault(Object key, V defaultValue); 
//getOrDefault() 方法获取指定 key 对应对 value，如果找不到 key ，则返回设置的默认值。
map.put(s.charAt(i), i)；
map.containsKey(s.charAt(i)); //return boolean
map.get(s.charAt(i)); //return I
map.put(c, map.getOrDefault(c, 0) + 1);
//获取字符c的对应value或者c不在map，把c放到map并设置初始值1
```
4. Queue相关：
```java
Queue<TreeNode> q = new LinkedList<>();
Queue<TreeNode> queue = new ArrayDeque<>();
queue.add(); //在队列的最后面添加元素
queue.size(); //返回queue中元素个数
queue.poll(); //返回queue的最前端元素
!queue.isEmpty(); //queue不为空时
```
5. List相关：
```java
 List<List<Integer>> res = new ArrayList<>(); //二维动态数组
 List<Integer> res = new ArrayList<>();
 res.add(node.val);
 res.get(i); //返回res第i位的数值
 res.size();
```
6. Stack相关：
```java
//用Linkedlist实现stack
LinkedList<Integer> stack = new LinkedList<Integer>();
stack.addLast(head.val);
stack.removeLast();
//用ArrayDeque实现stack
Deque<Integer> stack = new ArrayDeque<Integer>();
stack.push(value);
stack.isEmpty();
stack.pop();
stack.peek(); //返回栈顶元素，但是不弹出
Stack<Treenode> stack = new Stack<>();
stack.push();
stack.pop();
!stack.isEmpty(); //stack不为空时
```
7. Math.max(a,b) 取最大值
8. 创建存放字母出现次数的数组：
```java
int[] list = new int[26];
++list[s.charAt(i) - 'a']; //字母对应的位置+1
```
9. 树相关：
```java
TreeNode node = new TreeNode(-1);
```
10. Array相关：
```java
Arrays.copyOfRange(int[], int from…, int to…);
//Arrays.copyOfRange(arr, 0, k);
Arrays.sort(arr);
for (int i = 0; i < nums.length; i++); //等价于
for (int num : nums);
```
11. HashSet相关：
```java
HashSet<ListNode> set = new HashSet<>();
set.contains(node);
set.add(node);
```
12. ListNode dummyNode = new ListNode(-1);
13. 三目运算：prev.next = (l1 == null) ? l2 : l1;