### Intro

<img width="604" height="258" alt="image" src="https://github.com/user-attachments/assets/ff8b14b0-3dee-405d-b872-7c47027d01f5" />
<img width="1127" height="320" alt="image" src="https://github.com/user-attachments/assets/e896534f-0bb4-41dd-9f01-2fce11509ec4" />
<img width="1009" height="413" alt="image" src="https://github.com/user-attachments/assets/ca4f5ff8-e9cd-40bd-bbc9-04f77825869b" />
<img width="714" height="451" alt="image" src="https://github.com/user-attachments/assets/4750527f-de29-45b2-94c5-194c3bedf41e" />
If the Sibling Subtress are swapped , it is still a min Heap.
<img width="754" height="450" alt="image" src="https://github.com/user-attachments/assets/184cf915-84e5-44f9-b4f4-63854a46e452" />
<img width="925" height="224" alt="image" src="https://github.com/user-attachments/assets/2e657542-6768-40e0-8354-695e64b2dcc0" />

<img width="1068" height="580" alt="image" src="https://github.com/user-attachments/assets/dc0df254-701d-4f91-a18e-2b8e7008da7e" />
<img width="1057" height="584" alt="image" src="https://github.com/user-attachments/assets/f6e84e75-dd22-45d4-b56e-5ae13635f5e1" />
<img width="778" height="490" alt="image" src="https://github.com/user-attachments/assets/584e357a-3076-4b26-a8ca-afe714b9b635" />
<img width="1043" height="401" alt="image" src="https://github.com/user-attachments/assets/ddf4f0bb-3792-4ba4-ab84-42dffd092c9c" />


<img width="793" height="207" alt="image" src="https://github.com/user-attachments/assets/8b5503c7-f5d9-4503-a490-55f2a5efcd60" />
<img width="978" height="498" alt="image" src="https://github.com/user-attachments/assets/4b226e32-9670-43e8-aa6a-37afdfdbd4a2" />
<img width="684" height="472" alt="image" src="https://github.com/user-attachments/assets/af373d8a-7e16-478a-80d6-792c09b4b540" />

#### First 2 problems show how to implement a Heap, Interviews most likely do not need this implmentation. For Interview check how to Use Java Priority Queues for Heaps. (Problem 3 and 4)

### Heap Insertion
<img width="332" height="155" alt="image" src="https://github.com/user-attachments/assets/04fd3350-a29b-40fb-ad2d-effab75c4214" />. 

<img width="666" height="409" alt="image" src="https://github.com/user-attachments/assets/6ce1075f-446b-49c3-bdd0-450b45113fef" />
<img width="644" height="415" alt="image" src="https://github.com/user-attachments/assets/28d68453-8472-4523-97e6-f7c54ebf09f3" />
<img width="399" height="212" alt="image" src="https://github.com/user-attachments/assets/8b3379b5-2a89-4fe9-8abc-961ca962cde7" />
<img width="608" height="295" alt="image" src="https://github.com/user-attachments/assets/2409fad8-45c6-4b6f-923b-5211cb5d31e7" />
<img width="609" height="259" alt="image" src="https://github.com/user-attachments/assets/bf7048ac-2520-42ea-8ea0-8f62f5126c45" />
<img width="596" height="273" alt="image" src="https://github.com/user-attachments/assets/08d18dc5-ea63-4cff-8379-349283e43ddf" />

```
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

### Heap deletion



```
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


### 

kth-largest
Write a method, kthLargest, that takes in a list of numbers and a value, k. The method should return the k-th largest element of the list.

kthLargest(List.of(9,2,6,6,1,5,8,7), 3); // -> 7


Solution 1: Using Sorting
<img width="585" height="365" alt="image" src="https://github.com/user-attachments/assets/dcdf98b6-26c0-4074-a1a0-a4e0d49a75ec" />

Ideal Solution : Using Heap
We do not need to fully sort. Parial Sorting using Heap is sufficient, since we can get better Time Complexity with heaps
<img width="662" height="130" alt="image" src="https://github.com/user-attachments/assets/97a602af-bbca-41b1-8c99-e67b2fcffc23" />
<img width="662" height="412" alt="image" src="https://github.com/user-attachments/assets/7de7be3a-b21b-484c-b1c0-579720d40828" />

```
public static int kthLargest(List<Integer> numbers, int k) {
    List<Integer> sortedNumbers = new ArrayList<>(numbers);
    Collections.sort(sortedNumbers);
    return sortedNumbers.get(sortedNumbers.size() - k);
  }
```

```
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

### k-smallest
Write a method that takes in a list of numbers and a value, k. The method should return the k smallest numbers in the list. The resulting list should be ordered from least to greatest.

kSmallest(List.of(8, 2, 7, -3, 5, 10), 3) ;
// -> [-3, 2, 5]

<img width="655" height="396" alt="image" src="https://github.com/user-attachments/assets/8b1eb310-b2a8-45a2-96a0-fd6a687ddd13" />

```
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


#### TIP
Min heap vs Max Heap
Min head contains Extract Min while max heap contains extract max. so if we want smaller numbers use max heap since we will be removing max numbers and what remains is small numbers and viceversa.














