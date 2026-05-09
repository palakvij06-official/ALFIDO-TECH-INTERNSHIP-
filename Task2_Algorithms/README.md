#include <iostream>
#include <algorithm>
using namespace std;

// ---------- MERGE SORT ----------
void merge(int arr[], int l, int m, int r) {
    int i = l, j = m+1, k = 0;
    int temp[100];

    while (i <= m && j <= r) {
        if (arr[i] < arr[j])
            temp[k++] = arr[i++];
        else
            temp[k++] = arr[j++];
    }

    while (i <= m) temp[k++] = arr[i++];
    while (j <= r) temp[k++] = arr[j++];

    for (i = l, k = 0; i <= r; i++, k++)
        arr[i] = temp[k];
}

void mergeSort(int arr[], int l, int r) {
    if (l < r) {
        int m = (l + r) / 2;
        mergeSort(arr, l, m);
        mergeSort(arr, m+1, r);
        merge(arr, l, m, r);
    }
}

// ---------- BINARY SEARCH ----------
int binarySearch(int arr[], int n, int key) {
    int l = 0, r = n-1;
    while (l <= r) {
        int mid = (l + r) / 2;
        if (arr[mid] == key) return mid;
        else if (arr[mid] < key) l = mid + 1;
        else r = mid - 1;
    }
    return -1;
}

// ---------- GREEDY (Activity Selection) ----------
struct Activity {
    int start, finish;
};

bool compare(Activity a, Activity b) {
    return a.finish < b.finish;
}

void activitySelection(Activity arr[], int n) {
    sort(arr, arr+n, compare);

    cout << "Selected Activities:\n";
    int i = 0;
    cout << "(" << arr[i].start << "," << arr[i].finish << ")\n";

    for (int j = 1; j < n; j++) {
        if (arr[j].start >= arr[i].finish) {
            cout << "(" << arr[j].start << "," << arr[j].finish << ")\n";
            i = j;
        }
    }
}

// ---------- MAIN ----------
int main() {
    int arr[] = {5, 2, 9, 1, 3};
    int n = 5;

    mergeSort(arr, 0, n-1);

    cout << "Sorted Array:\n";
    for (int i = 0; i < n; i++) cout << arr[i] << " ";

    cout << "\nBinary Search (key=3): " << binarySearch(arr, n, 3);

    Activity act[] = {{1,2}, {3,4}, {0,6}, {5,7}, {8,9}};
    activitySelection(act, 5);

    return 0;
}
