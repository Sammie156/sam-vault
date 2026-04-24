Quick Sort is a *divide-and-conquer* algorithm, and sorts *in-place*. 
It works by taking a `pivot` element and *partitions* the given array around the picked `pivot`. All the smaller elements are to the left of the `pivot`, while the larger elements are to the right.

## **Deterministic Quick Sort**:
1. *Divide*: Partition the array into two subarrays around a pivot `x`, such that lower elements are on the lower subarray, and the higher ones in the upper subarray.
2. *Conquer*: Recursively sort the two subarrays.
3. *Combine*: Combine all the subarrays so formed.

*C Code*:
```c
#include <stdio.h>

void swap(int* a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

int partition(int arr[], int low, int high) {
    int pivot = arr[high];

    int i = low - 1;

    for (int j = low; j < high; j++) {
        if (arr[j] < pivot) {
            i++;
            swap(&arr[i], &arr[j]);
        }
    }

    swap(&arr[i + 1], &arr[high]);
    return i + 1;
}

void quickSort(int arr[], int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high);

        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

int main(int argc, const char* argv[]) {
    int n;
    scanf("%d", &n);

    int arr[n];
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }

    quickSort(arr, 0, n - 1);

    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
}
```
**WORKING**:
![[20260423-2027-44.7605712.mp4]] 

### **Analysis of Quick Sort**:
- Assume all inputs are distinct.
- Let $T(n)$ is the worst-case running time on an array of $n$ elements.

The worst case scenario is that the input array is reverse sorted, i.e., there are no elements on one side of the array. This makes the time complexity: $O(n^{2})$.
The best case scenario is that the input array is split evenly. This makes the time complexity: $O(n\log n)$ . 
Hence, we can conclude:

> [!tip] Importance of Pivot
> The time complexity depends heavily on the pivot we choose.
> Bad pivot can lead to worse results.

## **Randomized Quick Sort**:
The idea of this is to pivot around a `random` element.
- Running time is independent of the input array.
- No assumptions need to made about the input distribution like we did before.
- The worst-case is determined only by the random number generator.

*C Code*:
```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

int generate_random(int low, int high) {
    srand(time(NULL));
    return low + rand() % (high - low + 1);
}

void quickSort(int arr[], int low, int high) {
    if (low < high) {
        int pivot = generate_random(low, high);
        int val = arr[pivot];

        swap(&arr[pivot], &arr[high]);

        int i = low - 1;

        for (int j = low; j < high; j++) {
            if (arr[j] < val) {
                i++;
                swap(&arr[i], &arr[j]);
            }
        }

        swap(&arr[i + 1], &arr[high]);

        quickSort(arr, low, i);
        quickSort(arr, i + 2, high);
    }
}

int main(int argc, const char* argv[]) {
    int n;
    scanf("%d", &n);

    int arr[n];
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }

    quickSort(arr, 0, n - 1);

    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
}
```
