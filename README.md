# lessons 8
# Сортировки C++
Основные виды сортировок:

    1. Сортировка пузырьком (Bubble Sort)
    2. Сортировка выбором (Selection Sort)
    3. Сортировка вставками (Insertion Sort)
    4. Быстрая сортировка (Quick Sort)
    5. Сортировка слиянием (Merge Sort)
    6. Пирамидальная сортировка (Heap Sort)
    
Вот пример простой реализации сортировки пузырьком на языке C++:
```C++
void bubbleSort(int* arr, int size) {
    for (int i = 0; i < size - 1; i++) {
        for (int j = 0; j < size - i - 1; j++) {
            if (arr[j] > arr[j+1]) {
                // int temp = arr[j];
                // arr[j] = arr[j+1];
                // arr[j+1] = temp;
                std::swap(arr[j], arr[j+1]);
            }
        }
    }
}
```
