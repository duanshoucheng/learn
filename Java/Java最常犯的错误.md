# 1. 数组转ArrayList  
为了实现把一个数组转换成一个ArrayList，很多Java程序员会使用如下的代码：
```
List<String> list = Arrays.asList(arr);
```
Arrays.asList确实会返回一个ArrayList对象，但该ArrayList类是Arrays内部中的一个私有静态内部类，而不是我们常用的java.util.ArrayList类。这个java.util.Arrays.ArrayList类具有 set()，get()，contains()等方法，但是不具有任何添加或移除元素的任何方法。因为该类的大小(size)是固定的。为了创建出一个真正的ArrayList，代码应该如下所示：
```
ArrayList<String> arrayList = new ArrayList<String>(Arrays.asList(arr));
```
我们知道，ArrayList的构造方法可以接受一个Collection类型的对象，而我们的 java.util.Arrays.ArrayList正好也是它的一个子类。实际上，更加高效的代码示例是：
```
ArrayList<String> arrayList = new ArrayList<String>(arr.length);
Collections.addAll(arrayList, arr);
```

# 2. 数组是否包含特定值
```
Set<String> set = new HashSet<String>(Arrays.asList(arr));
```
这种效率太低，List转Set过程太消耗性能，可以如下优化：
```
Arrays.asList(arr).contains(targetValue);
```
进一步优化：
```
for(String s: arr) {
    if(s.equals(targetValue))
        return true;
}
return false;
```

# 3. 在迭代时移除List中的元素
    ```
    ArrayList<String> list = new ArrayList<String>(Arrays.asList("a", "b", "c", "d"));
    for(int i = 0; i<list.size(); i++){
        list.remove(i);
    }
    System.out.println(list);
    ```
输出结果为：【b,d】
代码中存在一个非常严重的错误。当一个元素被移除时，该List的大小(size)就会缩减，同时也改变了索引的指向。所以，在迭代的过程中使用索引，将无法从List中正确地删除多个指定的元素。

你可能知道解决这个错误的方式之一是使用迭代器(iterator)。而且，你可能认为Java中的foreach语句与迭代器(iterator)是非常相似的，但实际情况并不是这样。我们考虑一下如下的示例代码：
```
ArrayList<String> list = new ArrayList<String>(Arrays.asList("a", "b", "c", "d"));
Iterator<String> iter = list.iterator();
while(iter.hasNext()){
    String s = iter.next();
    if(s.equals("a"))
        iter.remove();
}
```