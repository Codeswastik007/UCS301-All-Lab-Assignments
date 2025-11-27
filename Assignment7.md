###Question1
```cpp

#include <iostream>
#include <vector>
using namespace std;
void selectionSort(vector<int>& arr) {
    int n = arr.size();
    for(int i = 0; i < n-1; i++) {
        int minIndex = i;
        for(int j = i+1; j < n; j++) {
            if(arr[j] < arr[minIndex])
                minIndex = j;
        }
        swap(arr[i], arr[minIndex]);
    }
}

void insertionSort(vector<int>& arr) {
    int n = arr.size();
    for(int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        while(j >= 0 && arr[j] > key) {
            arr[j+1] = arr[j];
            j--;
        }
        arr[j+1] = key;
    }
}

void bubbleSort(vector<int>& arr) {
    int n = arr.size();
    for(int i = 0; i < n - 1; i++) {
          
        for(int j = 0; j < n - i - 1; j++) {
            if(arr[j] > arr[j + 1]) {
                swap(arr[j], arr[j + 1]);
                
            }
        }
         
    }
}

void merge(vector<int>& arr, int left, int mid, int right) {
    vector<int> temp;
    int i = left, j = mid+1;

    while(i <= mid && j <= right) {
        if(arr[i] < arr[j]) temp.push_back(arr[i++]);
        else temp.push_back(arr[j++]);
    }
    while(i <= mid) temp.push_back(arr[i++]);
    while(j <= right) temp.push_back(arr[j++]);

    for(int k = 0; k < temp.size(); k++)
        arr[left + k] = temp[k];
}

void mergeSort(vector<int>& arr, int left, int right) {
    if(left < right) {
        int mid = (left + right) / 2;
        mergeSort(arr, left, mid);
        mergeSort(arr, mid+1, right);
        merge(arr, left, mid, right);
    }
}
int partition(vector<int>& arr, int low, int high) {
    int pivot = arr[high];
    int i = low - 1;

    for(int j = low; j < high; j++) {
        if(arr[j] < pivot) {
            i++;
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i+1], arr[high]);
    return i+1;
}

void quickSort(vector<int>& arr, int low, int high) {
    if(low < high) {
        int p = partition(arr, low, high);
        quickSort(arr, low, p-1);
        quickSort(arr, p+1, high);
    }
}

void print(vector<int>& arr) {
    for(int x : arr) cout << x << " ";
    cout << endl;
}
int main() {
    vector<int> arr = {64, 25, 12, 22, 11};
    cout << "Original array: ";
    print(arr);
    selectionSort(arr);
    insertionSort(arr);
    bubbleSort(arr);
    mergeSort(arr, 0, arr.size()-1);
    quickSort(arr, 0, arr.size()-1);
    cout << "Sorted array: ";
    print(arr);

    return 0;
}
```

###Question 2
```cpp
#include <iostream>
#include <vector>
using namespace std;

void newSelectionSort(vector<int>& arr) {
    int left = 0, right = arr.size() - 1;

    while (left < right) {
        int minIndex = left;
        int maxIndex = right;

        for (int i = left; i <= right; i++) {
            if (arr[i] < arr[minIndex]) minIndex = i;
            if (arr[i] > arr[maxIndex]) maxIndex = i;
        }

        swap(arr[left], arr[minIndex]);

        if (maxIndex == left) maxIndex = minIndex;

        swap(arr[right], arr[maxIndex]);

        left++;
        right--;
    }
}

void print(vector<int>& arr) {
    for (int x : arr) cout << x << " ";
    cout << endl;
}
int main() {
    vector<int> arr = {64, 25, 12, 22, 11, 90, 3};
    newSelectionSort(arr);
    print(arr);
}
```

###Add1
```cpp
#include <bits/stdc++.h>
using namespace std;

int main(){
    int n;
    cin>>n;
    int a[n];
    for(int i=0;i<n;i++) cin>>a[i];
    int mn=a[0], mx=a[0];
    for(int i=1;i<n;i++){
        if(a[i]<mn) mn=a[i];
        if(a[i]>mx) mx=a[i];
    }
    int range = mx - mn + 1;
    int cnt[range];
    for(int i=0;i<range;i++) cnt[i]=0;
    for(int i=0;i<n;i++) cnt[a[i]-mn]++;
    for(int i=0;i<range;i++){
        while(cnt[i]--){
            cout<<i+mn<<" ";
        }
    }
    return 0;
}


```


###Add2
```cpp
#include <bits/stdc++.h>
using namespace std;

int getMax(int a[], int n){
    int mx = a[0];
    for(int i=1;i<n;i++) if(a[i]>mx) mx=a[i];
    return mx;
}

void countSort(int a[], int n, int exp){
    int output[n];
    int cnt[10];
    for(int i=0;i<10;i++) cnt[i]=0;
    for(int i=0;i<n;i++) cnt[(a[i]/exp)%10]++;
    for(int i=1;i<10;i++) cnt[i]+=cnt[i-1];
    for(int i=n-1;i>=0;i--){
        int digit=(a[i]/exp)%10;
        output[cnt[digit]-1] = a[i];
        cnt[digit]--;
    }
    for(int i=0;i<n;i++) a[i]=output[i];
}

void radixSort(int a[], int n){
    int mx = getMax(a,n);
    for(int exp=1; mx/exp>0; exp*=10)
        countSort(a,n,exp);
}

int main(){
    int n;
    cin>>n;
    int a[n];
    for(int i=0;i<n;i++) cin>>a[i];
    radixSort(a,n);
    for(int i=0;i<n;i++) cout<<a[i]<<" ";
    return 0;
}
```
