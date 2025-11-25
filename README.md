# -16
# 2.1
#include <stdio.h>
#include <stdlib.h>

// Функция удаления элемента по индексу
int delete_k(double* ptr_arr, int size, int k) {
    int n = size - 1;
    for (int i = k; i < (size - 1); i++)
        ptr_arr[i] = ptr_arr[i + 1];
    return n;
}

// Функция удаления элементов, значение которых превышает A
int delete_elements_greater_than_A(double* arr, int size, double A) {
    int new_size = size;
    int i = 0;
    
    while (i < new_size) {
        if (arr[i] > A) {
            // Удаляем элемент с индексом i
            new_size = delete_k(arr, new_size, i);
            // Не увеличиваем i, так как массив сдвинулся
        } else {
            i++;
        }
    }
    
    return new_size;
}

// Функция печати массива
void print_array(double* arr, int size) {
    printf("Массив: [");
    for (int i = 0; i < size; i++) {
        printf("%.2f", arr[i]);
        if (i < size - 1) printf(", ");
    }
    printf("]\n");
}

int main() {
    // Создаем и инициализируем массив
    double arr[] = {1.5, 3.2, 7.8, 2.1, 9.4, 0.5, 4.3};
    int size = sizeof(arr) / sizeof(arr[0]);
    
    printf("Исходный ");
    print_array(arr, size);
    
    double A = 4.0; // Пороговое значение
    printf("Удаляем элементы, превышающие %.2f\n", A);
    
    // Удаляем элементы, превышающие A
    int new_size = delete_elements_greater_than_A(arr, size, A);
    
    printf("Измененный ");
    print_array(arr, new_size);
    printf("Новый размер массива: %d\n", new_size);
    
    return 0;
}





#2.2

#include <stdio.h>
#include <stdlib.h>
#include <limits.h>

// Функция вставки элемента
int* insert(int* ptr_arr, int *size, int index, int num) {
    int size_n = (*size) + 1;
    
    if (ptr_arr == NULL) return NULL;
    
    int* ptr_arr_n = (int*)realloc(ptr_arr, size_n * sizeof(int));
    if (ptr_arr_n == NULL) return ptr_arr;
    
    ptr_arr = ptr_arr_n;
    
    // Сдвигаем элементы вправо, начиная с конца до позиции вставки
    for (int i = size_n - 1; i > index; i--)
        ptr_arr[i] = ptr_arr[i - 1];
    
    ptr_arr[index] = num;
    *size = size_n;
    return ptr_arr;
}

// Функция поиска индекса максимального элемента
int find_max_index(int* arr, int size) {
    int max_index = 0;
    int max_value = INT_MIN;
    
    for (int i = 0; i < size; i++) {
        if (arr[i] > max_value) {
            max_value = arr[i];
            max_index = i;
        }
    }
    
    return max_index;
}

// Функция вставки перед максимальным элементом
int* insert_before_max(int* arr, int* size) {
    int max_index = find_max_index(arr, *size);
    
    printf("Максимальный элемент: %d (индекс %d)\n", arr[max_index], max_index);
    
    // Вставляем -999 перед максимальным элементом
    arr = insert(arr, size, max_index, -999);
    
    return arr;
}

// Функция печати массива
void print_array(int* arr, int size) {
    printf("Массив: [");
    for (int i = 0; i < size; i++) {
        printf("%d", arr[i]);
        if (i < size - 1) printf(", ");
    }
    printf("]\n");
}

int main() {
    int size = 8;
    int* arr = (int*)malloc(size * sizeof(int));
    
    // Инициализируем массив случайными значениями
    int initial_values[] = {12, 45, 3, 78, 23, 56, 89, 34};
    for (int i = 0; i < size; i++) {
        arr[i] = initial_values[i];
    }
    
    printf("Исходный ");
    print_array(arr, size);
    
    // Вставляем -999 перед максимальным элементом
    arr = insert_before_max(arr, &size);
    
    printf("Измененный ");
    print_array(arr, size);
    printf("Новый размер массива: %d\n", size);
    
    free(arr);
    return 0;
}
