---
sort: 1
---

# Sorts
## QuickSort
``` cpp
int partition(int a[], int left, int right) {
  int pivot = --right; 
  while (true) {
    while (a[left] < a[pivot])
      ++left;
    while (left < right && a[right - 1] >= a[pivot]) 
      --right;
    if (left >= right)
      break;
    swap(a[left], a[right - 1]);
  }//while
  swap(a[left], a[pivot]);
  return left;
}
// partition()
```
``` cpp
void quicksort(int a[], int left, int right) {
    if (left + 1 >= right)
      return;
    int pivot = partition(a, left, right);
    if(pivot - left < right - pivot -1){//situation
      quicksort(a, left, pivot);
      quicksort(a, pivot + 1, right);
    }
    else{
      quicksort(a, pivot + 1, right);
      quicksort(a, left, pivot);
    }
} // quicksort()
```
## MergeSort
``` cpp
void merge(Item a[], int left, int mid, int right) { 
  int size = right - left;
  vector<int> c(size);
  for (int i = left, j = mid, k = 0; k < size; ++k) {
    if (i == mid)
        c[k] = a[j++]; 
    else if (j == right)
      c[k] = a[i++];
    else
      c[k] = (a[i] <= a[j]) ? a[i++] : a[j++];
  } // for
copy(c.begin(), c.end(), &a[left]); // merge()
}
```
``` cpp
void merge_sort(Item a[], int left, int right) {
  if (right < left + 2) // base case: < 2 items 
    return;
  int mid = left + (right - left) / 2;
  merge_sort(a, left, mid); // [left, mid) 
  merge_sort(a, mid, right); // [mid + 1, right) 
  merge(a, left, mid, right);
}// merge_sort()
```
## HeapSort
``` cpp
void heapify(int arr[], int n, int i) 
{ 
    int largest = i; // Initialize largest as root 
    int l = 2 * i + 1; // left = 2*i + 1 
    int r = 2 * i + 2; // right = 2*i + 2 
  
    // If left child is larger than root 
    if (l < n && arr[l] > arr[largest]) 
        largest = l; 
  
    // If right child is larger than largest so far 
    if (r < n && arr[r] > arr[largest]) 
        largest = r; 
  
    // If largest is not root 
    if (largest != i) { 
        swap(arr[i], arr[largest]); 
  
        // Recursively heapify the affected sub-tree 
        heapify(arr, n, largest); 
    } 
} 
```
``` cpp
void heapsort(Item heap[], int n) {
    heapify(heap, n);
    for (int i = n; i >= 2; --i) {
    swap(heap[i], heap[1]);
    fixDown(heap, i - 1, 1); 
    } // heapsort()
}
```
![avatar](/home/Interviews/pic/sort.png)