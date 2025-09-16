# Problem: Time Based Key Value Store

## 📄 Problem Statement
Design a time-based key-value data structure that can store multiple values for the same key at different 
time stamps and retrieve the key's value at a certain timestamp.

---

## 🧠 Brute Force Approach
### Idea
- Map<String, TreeMap<Integer, String>>
- <Key, <Version, Value>>
- All entries part of treemap are of sorted fashion (version - integer)
- retrieval from tree map is of time complexity O(n)

### Code
```java
// Brute force solution
class TimeMap {
    // key          version, value
    Map<String, TreeMap<Integer, String>> store;

    public TimeMap() {
        store = new HashMap<>();
    }

    public void set(String key, String value, int timestamp) {
        store.computeIfAbsent(key, x-> new TreeMap<>()).put(timestamp, value);
    }

    public String get(String key, int timestamp) {
        Integer version = (store.containsKey(key)) ? store.get(key).floorKey(timestamp) : null;
        return version!=null ? store.get(key).get(version) : "";
    }
}

```

### Complexity
- **Time:** O(logn)
- **Space:**
- 
---

## ✅ Key Takeaways
- TreeMap in Java