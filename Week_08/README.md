学习笔记

本周学习了位运算、布隆过滤器、LRU缓存机制、还有各种排序。
视频内容将知识点复习了一变，一些高级数据结构也第一次接触，解题目的思路还是比较弱，后面加强练习。  

##布隆过滤器
布隆过滤器其实就是将一个对象经过多次hash函数之后,将其映射到一个很长的二进制位上.
布隆过滤器的特点就是查询效率非常高,存储内存都非常低
所以布隆过滤器经常被用于一些邮件黑名单等等.
使用布隆过滤器可以很好的判断一个对象是否在系统不存在,但是只能判断一个对象可能存在,不能确定.

##LRUCache
是最近最少使用的淘汰算法.
使用HashMap和双向链表可以实现.
````
public class LRUCache {

    private Map<Integer,Node> cache = new HashMap<>();
    private int size;
    private int capacity;
    private Node head,tail;

    public LRUCache(int capacity) {
        this.size = 0;
        this.capacity = capacity;
        head = new Node();
        tail = new Node();
        head.next = tail;
        tail.prev = head;
    }

    public int get(int key) {
        Node node = cache.get(key);
        if(node == null){
            return -1;
        }
        moveToHead(node);
        return node.value;
    }

    public void put(int key, int value) {
        Node node = cache.get(key);

        if(node == null){
            Node currNode = new Node(key,value);
            cache.put(key,currNode);
            addToHead(currNode);
            size ++;
            if(size > capacity){
                Node delete = removeTail();
                cache.remove(delete.key);
                size --;
            }
        }else{
            node.value = value;
            moveToHead(node);
        }
    }

    private Node removeTail() {
        Node res = tail.prev;
        removeNode(res);
        return res;
    }

    private void removeNode(Node node){
        node.prev.next = node.next;
        node.next.prev = node.prev;
    }

    private void addToHead(Node node) {
        node.prev = head;
        node.next = head.next;
        head.next.prev = node;
        head.next = node;
    }

    private void moveToHead(Node node) {
        removeNode(node);
        addToHead(node);
    }

    public class Node{
        private int key;
        private int value;

        private Node prev;
        private Node next;

        public Node(){

        }

        public Node(int key, int value){
            this.key = key;
            this.value = value;
        }
    }

}
````

##排序算法
最基础的就是 选择 冒泡 插入排序 时间复杂度是O(n^2)

高级一点的排序有: 1. 快速排序,分治思想 2. 归并排序,分治思想 3. 堆排序,利用系统的大根堆或是小根堆 4. 希尔排序 5. 计数排序 6. 桶排序 7. 基数排序