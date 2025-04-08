
# DAA Lab Exam

Prepared by Usham Roy

## 1. Insertion Sort

```c
#include &lt;stdio.h&gt;

void insertionSort(int arr[], int n) {
    int i, key, j;
    for (i = 1; i &lt; n; i++) {
        key = arr[i];  // Take the current element
        j = i - 1;
        
        // Move elements that are greater than key to one position ahead
        while (j &gt;= 0 &amp;&amp; arr[j] &gt; key) {
            arr[j + 1] = arr[j];
            j = j - 1;
        }
        arr[j + 1] = key;  // Place key at its correct position
    }
}

int main() {
    int n, i;
    printf("Enter the number of elements: ");
    scanf("%d", &amp;n);
    
    int arr[n];
    printf("Enter %d elements: ", n);
    for(i = 0; i &lt; n; i++)
        scanf("%d", &amp;arr[i]);
    
    insertionSort(arr, n);
    
    printf("Sorted array: ");
    for(i = 0; i &lt; n; i++)
        printf("%d ", arr[i]);
    
    return 0;
}
```

**Explanation**: Insertion sort builds the final sorted array one item at a time. It iterates through an array, consuming one input element at each repetition, and growing a sorted output list. For each iteration, insertion sort removes one element from the input data, finds its location in the sorted list, and inserts it there. Time complexity is O(n²) in worst case, but efficient for small data sets.

## 2. Bubble Sort

```c
#include &lt;stdio.h&gt;

void bubbleSort(int arr[], int n) {
    int i, j, temp;
    for (i = 0; i &lt; n-1; i++) {
        // Last i elements are already in place
        for (j = 0; j &lt; n-i-1; j++) {
            // Compare adjacent elements
            if (arr[j] &gt; arr[j+1]) {
                // Swap if they are in wrong order
                temp = arr[j];
                arr[j] = arr[j+1];
                arr[j+1] = temp;
            }
        }
    }
}

int main() {
    int n, i;
    printf("Enter the number of elements: ");
    scanf("%d", &amp;n);
    
    int arr[n];
    printf("Enter %d elements: ", n);
    for(i = 0; i &lt; n; i++)
        scanf("%d", &amp;arr[i]);
    
    bubbleSort(arr, n);
    
    printf("Sorted array: ");
    for(i = 0; i &lt; n; i++)
        printf("%d ", arr[i]);
    
    return 0;
}
```

**Explanation**: Bubble Sort repeatedly steps through the list, compares adjacent elements, and swaps them if they're in the wrong order. The algorithm gets its name because smaller elements "bubble" to the top of the list. The process is repeated until no more swaps are needed. Time complexity is O(n²) in worst and average cases.

## 3. Linear Search

```c
#include &lt;stdio.h&gt;

int linearSearch(int arr[], int n, int key) {
    int i;
    for (i = 0; i &lt; n; i++) {
        if (arr[i] == key)
            return i;  // Return index if element found
    }
    return -1;  // Return -1 if element not found
}

int main() {
    int n, key, i, result;
    
    printf("Enter the number of elements: ");
    scanf("%d", &amp;n);
    
    int arr[n];
    printf("Enter %d elements: ", n);
    for(i = 0; i &lt; n; i++)
        scanf("%d", &amp;arr[i]);
    
    printf("Enter the element to search: ");
    scanf("%d", &amp;key);
    
    result = linearSearch(arr, n, key);
    
    if(result == -1)
        printf("Element not found");
    else
        printf("Element found at index %d", result);
    
    return 0;
}
```

**Explanation**: Linear Search is the simplest search algorithm that checks each element of the array until it finds a match or reaches the end. It works on both sorted and unsorted arrays. Time complexity is O(n) in worst case.

## 4. Binary Search

```c
#include &lt;stdio.h&gt;

int binarySearch(int arr[], int low, int high, int key) {
    if (high &gt;= low) {
        int mid = low + (high - low) / 2;  // Calculate middle point
        
        // If element is present at the middle
        if (arr[mid] == key)
            return mid;
        
        // If element is smaller than mid, search in left subarray
        if (arr[mid] &gt; key)
            return binarySearch(arr, low, mid - 1, key);
        
        // Else search in right subarray
        return binarySearch(arr, mid + 1, high, key);
    }
    
    return -1;  // Element not found
}

int main() {
    int n, key, i, result;
    
    printf("Enter the number of elements: ");
    scanf("%d", &amp;n);
    
    int arr[n];
    printf("Enter %d elements in sorted order: ", n);
    for(i = 0; i &lt; n; i++)
        scanf("%d", &amp;arr[i]);
    
    printf("Enter the element to search: ");
    scanf("%d", &amp;key);
    
    result = binarySearch(arr, 0, n-1, key);
    
    if(result == -1)
        printf("Element not found");
    else
        printf("Element found at index %d", result);
    
    return 0;
}
```

**Explanation**: Binary Search works on sorted arrays by repeatedly dividing the search range in half. If the value being searched is less than the middle element, continue in the lower half; otherwise, continue in the upper half. Time complexity is O(log n), making it much faster than linear search for large datasets.

## 5. Merge Sort

```c
#include &lt;stdio.h&gt;

void merge(int arr[], int l, int m, int r) {
    int i, j, k;
    int n1 = m - l + 1;
    int n2 = r - m;
    
    // Create temporary arrays
    int L[n1], R[n2];
    
    // Copy data to temporary arrays
    for (i = 0; i &lt; n1; i++)
        L[i] = arr[l + i];
    for (j = 0; j &lt; n2; j++)
        R[j] = arr[m + 1 + j];
    
    // Merge the temporary arrays back into arr[l..r]
    i = 0;  // Initial index of first subarray
    j = 0;  // Initial index of second subarray
    k = l;  // Initial index of merged subarray
    
    while (i &lt; n1 &amp;&amp; j &lt; n2) {
        if (L[i] &lt;= R[j]) {
            arr[k] = L[i];
            i++;
        } else {
            arr[k] = R[j];
            j++;
        }
        k++;
    }
    
    // Copy the remaining elements of L[]
    while (i &lt; n1) {
        arr[k] = L[i];
        i++;
        k++;
    }
    
    // Copy the remaining elements of R[]
    while (j &lt; n2) {
        arr[k] = R[j];
        j++;
        k++;
    }
}

void mergeSort(int arr[], int l, int r) {
    if (l &lt; r) {
        // Same as (l+r)/2, but avoids overflow for large l and r
        int m = l + (r - l) / 2;
        
        // Sort first and second halves
        mergeSort(arr, l, m);
        mergeSort(arr, m + 1, r);
        
        // Merge the sorted halves
        merge(arr, l, m, r);
    }
}

int main() {
    int n, i;
    printf("Enter the number of elements: ");
    scanf("%d", &amp;n);
    
    int arr[n];
    printf("Enter %d elements: ", n);
    for(i = 0; i &lt; n; i++)
        scanf("%d", &amp;arr[i]);
    
    mergeSort(arr, 0, n-1);
    
    printf("Sorted array: ");
    for(i = 0; i &lt; n; i++)
        printf("%d ", arr[i]);
    
    return 0;
}
```

**Explanation**: Merge Sort is an efficient, divide-and-conquer algorithm. It divides the array into two halves, recursively sorts them, and then merges the sorted halves. The merge operation is the key process that assumes the sub-arrays are sorted and merges them to produce a single sorted array. Time complexity is O(n log n) in all cases.

## 6. Quick Sort

```c
#include &lt;stdio.h&gt;

void swap(int* a, int* b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

int partition(int arr[], int low, int high) {
    int pivot = arr[high];  // Select the last element as pivot
    int i = (low - 1);      // Index of smaller element
    
    for (int j = low; j &lt;= high - 1; j++) {
        // If current element is smaller than the pivot
        if (arr[j] &lt; pivot) {
            i++;
            swap(&amp;arr[i], &amp;arr[j]);
        }
    }
    swap(&amp;arr[i + 1], &amp;arr[high]);
    return (i + 1);
}

void quickSort(int arr[], int low, int high) {
    if (low &lt; high) {
        // pi is partitioning index
        int pi = partition(arr, low, high);
        
        // Separately sort elements before and after partition
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

int main() {
    int n, i;
    printf("Enter the number of elements: ");
    scanf("%d", &amp;n);
    
    int arr[n];
    printf("Enter %d elements: ", n);
    for(i = 0; i &lt; n; i++)
        scanf("%d", &amp;arr[i]);
    
    quickSort(arr, 0, n-1);
    
    printf("Sorted array: ");
    for(i = 0; i &lt; n; i++)
        printf("%d ", arr[i]);
    
    return 0;
}
```

**Explanation**: Quick Sort is another divide-and-conquer algorithm that picks an element as a pivot and partitions the array around the selected pivot. In this implementation, we choose the last element as the pivot. The algorithm partitions the array so that all elements less than the pivot are on its left and all greater elements are on its right. Average time complexity is O(n log n), but worst case is O(n²).

## 7. Finding Maximum and Minimum in an Array

```c
#include &lt;stdio.h&gt;

void findMinMax(int arr[], int n, int* min, int* max) {
    // Initialize min and max with first element
    *min = *max = arr[^0];
    
    // Traverse array to find actual min and max
    for (int i = 1; i &lt; n; i++) {
        if (arr[i] &lt; *min)
            *min = arr[i];
        if (arr[i] &gt; *max)
            *max = arr[i];
    }
}

int main() {
    int n, i, min, max;
    printf("Enter the number of elements: ");
    scanf("%d", &amp;n);
    
    int arr[n];
    printf("Enter %d elements: ", n);
    for(i = 0; i &lt; n; i++)
        scanf("%d", &amp;arr[i]);
    
    findMinMax(arr, n, &amp;min, &amp;max);
    
    printf("Minimum element is %d\n", min);
    printf("Maximum element is %d\n", max);
    
    return 0;
}
```

**Explanation**: This algorithm finds the minimum and maximum elements in an array by initializing min and max with the first element and then traversing the array once, updating them whenever a smaller or larger element is found. Time complexity is O(n) as we need to check each element exactly once.

## 8. Longest Common Subsequence (LCS)

```c
#include &lt;stdio.h&gt;
#include &lt;string.h&gt;

int max(int a, int b) {
    return (a &gt; b) ? a : b;
}

int lcs(char* X, char* Y, int m, int n) {
    int L[m+1][n+1];
    int i, j;
    
    // Build L[m+1][n+1] in bottom-up fashion
    for (i = 0; i &lt;= m; i++) {
        for (j = 0; j &lt;= n; j++) {
            if (i == 0 || j == 0)
                L[i][j] = 0;
            else if (X[i-1] == Y[j-1])
                L[i][j] = L[i-1][j-1] + 1;
            else
                L[i][j] = max(L[i-1][j], L[i][j-1]);
        }
    }
    
    // L[m][n] contains length of LCS
    return L[m][n];
}

int main() {
    char X[^100], Y[^100];
    
    printf("Enter first string: ");
    scanf("%s", X);
    
    printf("Enter second string: ");
    scanf("%s", Y);
    
    int m = strlen(X);
    int n = strlen(Y);
    
    printf("Length of LCS is %d", lcs(X, Y, m, n));
    
    return 0;
}
```

**Explanation**: The Longest Common Subsequence algorithm finds the longest subsequence common to two sequences. A subsequence is a sequence derived from another sequence by deleting some elements without changing the order of the remaining elements. This implementation uses dynamic programming with a 2D array to store intermediate results. Time complexity is O(m×n) where m and n are lengths of the input strings.

## 9. Breadth-First Search (BFS)

```c
#include &lt;stdio.h&gt;
#include &lt;stdlib.h&gt;

#define MAX 100

// Queue implementation for BFS
struct Queue {
    int items[MAX];
    int front;
    int rear;
};

struct Queue* createQueue() {
    struct Queue* q = (struct Queue*)malloc(sizeof(struct Queue));
    q-&gt;front = -1;
    q-&gt;rear = -1;
    return q;
}

int isEmpty(struct Queue* q) {
    return q-&gt;front == -1;
}

void enqueue(struct Queue* q, int value) {
    if (q-&gt;rear == MAX - 1)
        printf("Queue Overflow\n");
    else {
        if (q-&gt;front == -1)
            q-&gt;front = 0;
        q-&gt;rear++;
        q-&gt;items[q-&gt;rear] = value;
    }
}

int dequeue(struct Queue* q) {
    int item;
    if (isEmpty(q)) {
        printf("Queue is empty\n");
        item = -1;
    } else {
        item = q-&gt;items[q-&gt;front];
        q-&gt;front++;
        if (q-&gt;front &gt; q-&gt;rear) {
            q-&gt;front = q-&gt;rear = -1;
        }
    }
    return item;
}

// Graph representation using adjacency matrix
struct Graph {
    int vertices;
    int* visited;
    int** adjMatrix;
};

// Create a graph with v vertices
struct Graph* createGraph(int v) {
    struct Graph* graph = (struct Graph*)malloc(sizeof(struct Graph));
    graph-&gt;vertices = v;
    graph-&gt;visited = (int*)malloc(v * sizeof(int));
    
    // Create adjacency matrix
    graph-&gt;adjMatrix = (int**)malloc(v * sizeof(int*));
    for (int i = 0; i &lt; v; i++) {
        graph-&gt;adjMatrix[i] = (int*)malloc(v * sizeof(int));
        for (int j = 0; j &lt; v; j++)
            graph-&gt;adjMatrix[i][j] = 0;
    }
    
    return graph;
}

// Add edge to graph
void addEdge(struct Graph* graph, int src, int dest) {
    // Add edge from src to dest
    graph-&gt;adjMatrix[src][dest] = 1;
    
    // Add edge from dest to src for undirected graph
    graph-&gt;adjMatrix[dest][src] = 1;
}

// BFS algorithm
void BFS(struct Graph* graph, int startVertex) {
    struct Queue* q = createQueue();
    
    // Mark start vertex as visited and enqueue it
    graph-&gt;visited[startVertex] = 1;
    printf("BFS traversal starting from vertex %d: ", startVertex);
    printf("%d ", startVertex);
    enqueue(q, startVertex);
    
    while (!isEmpty(q)) {
        // Dequeue a vertex and print it
        int currentVertex = dequeue(q);
        
        // Get all adjacent vertices of the dequeued vertex
        // If adjacent vertex is not visited, mark it visited and enqueue it
        for (int i = 0; i &lt; graph-&gt;vertices; i++) {
            if (graph-&gt;adjMatrix[currentVertex][i] == 1 &amp;&amp; !graph-&gt;visited[i]) {
                graph-&gt;visited[i] = 1;
                printf("%d ", i);
                enqueue(q, i);
            }
        }
    }
    printf("\n");
}

int main() {
    int v, e, src, dest, startVertex;
    
    printf("Enter number of vertices: ");
    scanf("%d", &amp;v);
    
    struct Graph* graph = createGraph(v);
    
    printf("Enter number of edges: ");
    scanf("%d", &amp;e);
    
    for (int i = 0; i &lt; e; i++) {
        printf("Enter edge (source destination): ");
        scanf("%d %d", &amp;src, &amp;dest);
        addEdge(graph, src, dest);
    }
    
    // Initialize visited array
    for (int i = 0; i &lt; v; i++)
        graph-&gt;visited[i] = 0;
    
    printf("Enter the starting vertex for BFS: ");
    scanf("%d", &amp;startVertex);
    
    BFS(graph, startVertex);
    
    return 0;
}
```

**Explanation**: Breadth-First Search explores all vertices at the present depth before moving on to vertices at the next depth level. It uses a queue data structure to keep track of vertices to be explored. This implementation represents the graph using an adjacency matrix. BFS is useful for finding the shortest path in unweighted graphs. Time complexity is O(V+E) where V is the number of vertices and E is the number of edges.

## 10. Depth-First Search (DFS)

```c
#include &lt;stdio.h&gt;
#include &lt;stdlib.h&gt;

// Graph representation using adjacency matrix
struct Graph {
    int vertices;
    int* visited;
    int** adjMatrix;
};

// Create a graph with v vertices
struct Graph* createGraph(int v) {
    struct Graph* graph = (struct Graph*)malloc(sizeof(struct Graph));
    graph-&gt;vertices = v;
    graph-&gt;visited = (int*)malloc(v * sizeof(int));
    
    // Create adjacency matrix
    graph-&gt;adjMatrix = (int**)malloc(v * sizeof(int*));
    for (int i = 0; i &lt; v; i++) {
        graph-&gt;adjMatrix[i] = (int*)malloc(v * sizeof(int));
        for (int j = 0; j &lt; v; j++)
            graph-&gt;adjMatrix[i][j] = 0;
    }
    
    return graph;
}

// Add edge to graph
void addEdge(struct Graph* graph, int src, int dest) {
    // Add edge from src to dest
    graph-&gt;adjMatrix[src][dest] = 1;
    
    // Add edge from dest to src for undirected graph
    graph-&gt;adjMatrix[dest][src] = 1;
}

// DFS algorithm
void DFS(struct Graph* graph, int vertex) {
    graph-&gt;visited[vertex] = 1;
    printf("%d ", vertex);
    
    for (int i = 0; i &lt; graph-&gt;vertices; i++) {
        if (graph-&gt;adjMatrix[vertex][i] == 1 &amp;&amp; !graph-&gt;visited[i]) {
            DFS(graph, i);
        }
    }
}

int main() {
    int v, e, src, dest, startVertex;
    
    printf("Enter number of vertices: ");
    scanf("%d", &amp;v);
    
    struct Graph* graph = createGraph(v);
    
    printf("Enter number of edges: ");
    scanf("%d", &amp;e);
    
    for (int i = 0; i &lt; e; i++) {
        printf("Enter edge (source destination): ");
        scanf("%d %d", &amp;src, &amp;dest);
        addEdge(graph, src, dest);
    }
    
    // Initialize visited array
    for (int i = 0; i &lt; v; i++)
        graph-&gt;visited[i] = 0;
    
    printf("Enter the starting vertex for DFS: ");
    scanf("%d", &amp;startVertex);
    
    printf("DFS traversal starting from vertex %d: ", startVertex);
    DFS(graph, startVertex);
    
    return 0;
}
```

**Explanation**: Depth-First Search explores as far as possible along each branch before backtracking. This implementation uses recursion to traverse the graph. DFS is useful for topological sorting, detecting cycles, and pathfinding applications. Time complexity is O(V+E) where V is the number of vertices and E is the number of edges.

## 11. Randomized Quicksort

```c
#include &lt;stdio.h&gt;
#include &lt;stdlib.h&gt;
#include &lt;time.h&gt;

void swap(int* a, int* b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

int randomPartition(int arr[], int low, int high) {
    // Generate a random number between low and high
    srand(time(NULL));
    int random = low + rand() % (high - low);
    
    // Swap the randomly selected element with the last element
    swap(&amp;arr[random], &amp;arr[high]);
    
    // Use the standard partition method
    int pivot = arr[high];
    int i = low - 1;
    
    for (int j = low; j &lt;= high - 1; j++) {
        if (arr[j] &lt; pivot) {
            i++;
            swap(&amp;arr[i], &amp;arr[j]);
        }
    }
    swap(&amp;arr[i + 1], &amp;arr[high]);
    return (i + 1);
}

void randomQuickSort(int arr[], int low, int high) {
    if (low &lt; high) {
        // pi is partitioning index
        int pi = randomPartition(arr, low, high);
        
        // Separately sort elements before and after partition
        randomQuickSort(arr, low, pi - 1);
        randomQuickSort(arr, pi + 1, high);
    }
}

int main() {
    int n, i;
    printf("Enter the number of elements: ");
    scanf("%d", &amp;n);
    
    int arr[n];
    printf("Enter %d elements: ", n);
    for(i = 0; i &lt; n; i++)
        scanf("%d", &amp;arr[i]);
    
    randomQuickSort(arr, 0, n-1);
    
    printf("Sorted array: ");
    for(i = 0; i &lt; n; i++)
        printf("%d ", arr[i]);
    
    return 0;
}
```

**Explanation**: Randomized Quicksort is a variation of Quick Sort where the pivot element is chosen randomly instead of always picking the last element. This randomization helps avoid the worst-case time complexity that regular Quicksort can experience with already sorted or nearly sorted arrays. By selecting a random pivot, the chance of consistently bad partitioning is reduced. The expected time complexity remains O(n log n).

Each of these implementations is optimized for clarity and simplicity, making them suitable for a lab exam. They include proper input handling and clear explanations of the algorithm's functionality.

<div>⁂</div>

[^1]: https://pplx-res.cloudinary.com/image/upload/v1744099646/user_uploads/gmuJCFXdvOdtBTW/WhatsApp-Image-2025-04-06-at-16.26.25.jpg

