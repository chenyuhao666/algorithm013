学习笔记

本周主要学习了字典树Trie 和 并查集,由于时间问题，红黑树章节还没看完。  
我自己尝试封装了下  
##Trie
````
public class Trie {

    Trie[] children  = new Trie[26];
    boolean isEndOfWord = false;

    /** Initialize your data structure here. */
    public Trie() {

    }

    /** Inserts a word into the trie. */
    public void insert(String word) {
        Trie tmp = this;
        for(char c : word.toCharArray()){
            if(tmp.children[c-'a'] == null){
                tmp.children[c-'a'] = new Trie();
            }
            tmp = tmp.children[c-'a'];
        }
        tmp.isEndOfWord = true;
    }

    /** Returns if the word is in the trie. */
    public boolean search(String word) {
        Trie tmp = this;
        for(char c : word.toCharArray()){
            if(tmp.children[c-'a'] == null){
                return false;
            }
            tmp = tmp.children[c-'a'];
        }
        return tmp.isEndOfWord;
    }

    /** Returns if there is any word in the trie that starts with the given prefix. */
    public boolean startsWith(String prefix) {
        Trie tmp = this;
        for(char c : prefix.toCharArray()){
            if(tmp.children[c-'a'] == null){
                return false;
            }
            tmp = tmp.children[c-'a'];
        }
        return true;
    }

}
````
##并查集
````
public class UnionFind {

    private int count;
    private int[] parent;
    private int[] size;

    public UnionFind(int n){
        this.count = n;
        this.parent = new int[n];
        this.size = new int[n];
        for(int i = 0 ; i < n ; i ++){
            parent[i] = i;
            size[i] =1;
        }
    }

    public void union(int p, int q){
        int rootP = find(p);
        int rootQ = find(q);
        if(rootP == rootQ){
            return;
        }

        if(size[rootP] > size[rootQ]){
            parent[rootQ] = rootP;
            size[rootP] +=size[rootQ];
        }else{
            parent[rootP] = rootQ;
            size[rootQ] += size[rootP];
        }
        count --;
    }

    private int find(int x){
        while(parent[x] != x){
            parent[x] = parent[parent[x]];
            x = parent[x];
        }
        return x;
    }

    public int count(){
        return count;
    }

}
````

高级搜素部分，主要学了剪枝和双向BFS，又把之前的题目重新刷了一遍。