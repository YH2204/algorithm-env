void shellSort(int a[], int n, int *comparisons, int *moves) {
    for (int gap = n / 2; gap >= 1; gap /= 2) {
        for (int i = gap; i < n; i++) {
            int key = a[i];
            (*moves)++;
            int j = i - gap;
            while (j >= 0) {
                (*comparisons)++;
                if (a[j] <= key) {
                    break;
                }
                a[j + gap] = a[j];
                (*moves)++;
                j -= gap;
            }
            a[j + gap] = key;
            (*moves)++;
        }
    }
}
