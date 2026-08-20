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























