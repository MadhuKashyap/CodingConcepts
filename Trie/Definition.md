### What is Trie  ?
The Trie data structure is a tree-like data structure used for storing a dynamic set of strings. It is commonly used for efficient retrieval and storage of keys in a large dataset. 

### Basic Operations
1. Insertion
2. Deletion
3. Searching
4. Traversal

### Trie Structure
```
public class Trie {
    Trie[] child;
    boolean isEnd;

    public Trie() {
        this.child = new Trie[26];
        this.isEnd = false;
    }
}
```

### Trie Operations

#### Insertion
```
public class TrieInsertion {
    public static void main(String[] args) {
        Trie t = new Trie();
        insert(t, "cat");
        insert(t, "catch");
        insert(t, "dog");
        insert(t, "dodge");
    }
    public static void insert(Trie t, String s) {
        Trie crawler = t;
        for(int i = 0; i < s.length(); i++) {
            if(crawler.child[s.charAt(i) - 'a'] == null) {
                crawler.child[s.charAt(i) - 'a'] = new Trie();
            }
            crawler = crawler.child[s.charAt(i) - 'a'];
        }
        crawler.isEnd = true;
    }
}

```
#### Traversal

```
public static void display(Trie t, StringBuilder s) {
        if(t == null)
            return;
        if(t.isEnd == true)
            System.out.println(s);
        for(int i = 0; i < 26; i++) {
            if(t.child[i] != null) {
                s.append((char)(i + 'a'));
                display(t.child[i], s);
                s.deleteCharAt(s.length() - 1);
            }
        }
    }
```

### Search

```
public static boolean search(Trie t, String word) {
        Trie crawler = t;
        for(int i = 0; i < word.length(); i++) {
            if(crawler.child[word.charAt(i) - 'a'] == null)
                return false;
            crawler = crawler.child[word.charAt(i) - 'a'];
        }
        return crawler.isEnd;
    }
```
