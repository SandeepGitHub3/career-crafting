# Heaps

## Index
- [Intro](#intro)
- [Tips](#tips)
- [Problems](#problems)
  - [1. Heap Insertion](#1-heap-insertion)
  - [2. Heap Deletion](#2-heap-deletion)
  - [3. Kth Largest Element](#3-kth-largest-element)
  - [4. K Smallest Elements](#4-k-smallest-elements)

---

## Intro

**What is a Heap?**
- binary tree data structure
- stores items
- maintains order between items
- similar to Binary Search Tree

**Ordering rules:**
- Binary Search Tree: all values left of a parent < parent; all values right of a parent ≥ parent
- Min Heap: parent nodes ≤ their children
- Max Heap: parent nodes ≥ their children

<img width="1009" height="413" alt="image" src="https://github.com/user-attachments/assets/ca4f5ff8-e9cd-40bd-bbc9-04f77825869b" />

<img width="714" height="451" alt="image" src="https://github.com/user-attachments/assets/4750527f-de29-45b2-94c5-194c3bedf41e" />

If the Sibling Subtress are swapped, it is still a min Heap.
<img width="754" height="450" alt="image" src="https://github.com/user-attachments/assets/184cf915-84e5-44f9-b4f4-63854a46e452" />

<img width="925" height="224" alt="image" src="https://github.com/user-attachments/assets/2e657542-6768-40e0-8354-695e64b2dcc0" />

**Complete Binary Tree** — 
- upper levels fully filled ✔,
- bottom-level nodes pushed as far left as possible ✔ (3 leftmost nodes on last row).

<img width="1068" height="580" alt="image" src="https://github.com/user-attachments/assets/dc0df254-701d-4f91-a18e-2b8e7008da7e" />
<img width="1057" height="584" alt="image" src="https://github.com/user-attachments/assets/f6e84e75-dd22-45d4-b56e-5ae13635f5e1" />
<img width="778" height="490" alt="image" src="https://github.com/user-attachments/assets/584e357a-3076-4b26-a8ca-afe714b9b635" />
<img width="1043" height="401" alt="image" src="https://github.com/user-attachments/assets/ddf4f0bb-3792-4ba4-ab84-42dffd092c9c" />
<img width="793" height="207" alt="image" src="https://github.com/user-attachments/assets/8b5503c7-f5d9-4503-a490-55f2a5efcd60" />
<img width="978" height="498" alt="image" src="https://github.com/user-attachments/assets/4b226e32-9670-43e8-aa6a-37afdfdbd4a2" />
<img width="684" height="472" alt="image" src="https://github.com/user-attachments/assets/af373d8a-7e16-478a-80d6-792c09b4b540" />

---

## Tips

- The first 2 problems (Heap Insertion, Heap Deletion) show how to **implement** a heap from scratch — interviews most likely don't require this. For interviews, use **Java's `PriorityQueue`** for heaps (see Problems 3 and 4).
- **Min heap vs Max heap:** a min heap's `extractMin()` removes the smallest item; a max heap's `extractMax()` removes the largest. So if you want the **smaller** numbers to remain, use a **max heap** (you keep evicting the max); if you want the **larger** numbers to remain, use a **min heap** (you keep evicting the min).

---

## Problems

### 1. Heap Insertion

**How to represent a heap:** as an **array** ✔ (not a node/pointer class ✘).

<img width="332" height="155" alt="image" src="https://github.com/user-attachments/assets/04fd3350-a29b-40fb-ad2d-effab75c4214" />

**Array indexing:** for a node at index `i` → left child = `2i + 1`, right child = `2i + 2`.

<img width="666" height="409" alt="image" src="https://github.com/user-attachments/assets/6ce1075f-446b-49c3-bdd0-450b45113fef" />

**Parent formula:** for index `i` → parent = `floor((i - 1) / 2)`.

<img width="644" height="415" alt="image" src="https://github.com/user-attachments/assets/28d68453-8472-4523-97e6-f7c54ebf09f3" />

**Heap Insertion steps:**
- Add the new node to the left-most open position of the bottom level.
- Min heap: **"sift up"** the new node while it's less than its parent.
- Max heap: **"sift up"** the new node while it's greater than its parent.

<img width="399" height="212" alt="image" src="https://github.com/user-attachments/assets/8b3379b5-2a89-4fe9-8abc-961ca962cde7" />

**Worked example** — inserting `8` into `[7, 11, 10, ...]`: since child (8) < parent (11), swap them.

<img width="608" height="295" alt="image" src="https://github.com/user-attachments/assets/2409fad8-45c6-4b6f-923b-5211cb5d31e7" />

After the swap, `8` sits above `11` — keep checking upward against the next parent (`7`).

<img width="609" height="259" alt="image" src="https://github.com/user-attachments/assets/bf7048ac-2520-42ea-8ea0-8f62f5126c45" />

`8` is not less than `7`, so it stops — this repeated bubbling is **"sift up" / "percolate up"**.

<img width="596" height="273" alt="image" src="https://github.com/user-attachments/assets/08d18dc5-ea63-4cff-8379-349283e43ddf" />

```java
 static class MinHeap {
    public List<Double> list;

    public MinHeap() {
      list = new ArrayList<>();
    }

    public int size() {
      return list.size();
    }

    public boolean isEmpty() {
      return list.size() == 0;
    }

    public void insert(Double val) {
      list.add(val);
      siftUp(list.size()-1);
    }

    private void siftUp(int index){
      while(index>0){
        int parentIndex = Math.abs((index-1)/2);
        if(list.get(index)<list.get(parentIndex)){
          swap(parentIndex,index);
          index = parentIndex;
        }else{
          break;
        }
      }
    }

   private void swap(int parentIndex, int currIndex){
      Double tmp = list.get(parentIndex);
      list.set(parentIndex,list.get(currIndex));
      list.set(currIndex,tmp);
    }
  }
```

---

### 2. Heap Deletion

```java
 public Double extractMin() {
      if (this.isEmpty()) {
        return null;
      }

      if (this.size() == 1) {
        return this.list.remove(this.list.size() - 1);
      }

      Double value = this.list.get(0);
      Double lastVal = this.list.remove(this.list.size() - 1);
      this.list.set(0, lastVal);
      this.siftDown(0);
      return value;
    }

 public void siftDown(int idx) {
      int currentIdx = idx;
      while (currentIdx < this.size() - 1) {
        int leftChildIdx = currentIdx * 2 + 1;
        int rightChildIdx = currentIdx * 2 + 2;
        
        double leftChildVal = leftChildIdx >= this.size() ? Double.POSITIVE_INFINITY : this.list.get(leftChildIdx);
        double rightChildVal = rightChildIdx >= this.size() ? Double.POSITIVE_INFINITY : this.list.get(rightChildIdx);
        
        double smallerChildVal = leftChildVal < rightChildVal ? leftChildVal : rightChildVal;
        int smallerChildIdx = leftChildVal < rightChildVal ? leftChildIdx : rightChildIdx;

        if (this.list.get(currentIdx) > smallerChildVal) {
          this.swap(currentIdx, smallerChildIdx);
          currentIdx = smallerChildIdx;
        } else {
          break;
        }
      } 
    }

  public void swap(int idx1, int idx2) {
      Double temp = this.list.get(idx1);
      this.list.set(idx1, this.list.get(idx2));
      this.list.set(idx2, temp);
    }
```

---

### 3. Kth Largest Element

Write a method, `kthLargest`, that takes in a list of numbers and a value, `k`. The method should return the k-th largest element of the list.

```
kthLargest(List.of(9,2,6,6,1,5,8,7), 3); // -> 7
```


**Solution 1: Using Sorting** — Time `O(n log n)`, Space `O(n)`: fully sort, then index from the end.

<img width="585" height="365" alt="image" src="https://github.com/user-attachments/assets/dcdf98b6-26c0-4074-a1a0-a4e0d49a75ec" />

```java
public static int kthLargest(List<Integer> numbers, int k) {
    List<Integer> sortedNumbers = new ArrayList<>(numbers);
    Collections.sort(sortedNumbers);
    return sortedNumbers.get(sortedNumbers.size() - k);
  }
```

**Ideal Solution: Using a Heap** — we don't need to **fully sort**; **partially sorting** with a heap is enough and gives a better time complexity.

<img width="662" height="130" alt="image" src="https://github.com/user-attachments/assets/97a602af-bbca-41b1-8c99-e67b2fcffc23" />

Sort: `O(n log n)` time, `O(n)` space. Heap: `O(n log k)` time, `O(k)` space (since `k ≤ n`) — keep a size-`k` **min heap** of the largest values seen so far; its root ends up being the k-th largest.

<img width="662" height="412" alt="image" src="https://github.com/user-attachments/assets/7de7be3a-b21b-484c-b1c0-579720d40828" />

```java
public static int kthLargest(List<Integer> numbers, int k) {
    PriorityQueue<Integer> minHeap = new PriorityQueue<>();

    for (int num : numbers) {
      minHeap.add(num);
      if (minHeap.size() > k) {
        minHeap.poll();
      }
    }

    return minHeap.poll();
  }
```

---

### 4. K Smallest Elements

Write a method that takes in a list of numbers and a value, `k`. The method should return the k smallest numbers in the list. The resulting list should be ordered from least to greatest.

```
kSmallest(List.of(8, 2, 7, -3, 5, 10), 3);
// -> [-3, 2, 5]
```


Keep a size-`k` **max heap** (`k ≤ n`, `.insert()` / `.extractMax()`) — the largest of the "k smallest so far" sits at the root, ready to be evicted the moment a smaller number shows up.

<img width="655" height="396" alt="image" src="https://github.com/user-attachments/assets/8b1eb310-b2a8-45a2-96a0-fd6a687ddd13" />

```java
public static List<Integer> kSmallest(List<Integer> numbers, int k) {
    PriorityQueue<Integer> maxHeap = new PriorityQueue<>((a,b) -> Integer.compare(b,a));
    
    for(int number: numbers){
      maxHeap.add(number);
      if(maxHeap.size()>k) 
        maxHeap.poll();
    }

    List<Integer> result = new ArrayList<>();
    while (maxHeap.size() > 0) {
      result.add(maxHeap.poll());
    }
    
    Collections.reverse(result);
    return result;
  }
```

-----------------------
