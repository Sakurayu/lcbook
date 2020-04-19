# Reverse Order

```text
//sort from longest to shortest
    Arrays.sort(strs, new Comparator<String>() {
        public int compare(String s1, String s2) {
            return s2.length() - s1.length();
        }
    });
    
```

