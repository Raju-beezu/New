//SELECTION SORT
____________________

#include<stdio.h>
#include<math.h>
#include<stdlib.h>
#include<time.h>

void selection_sort(int a[], int n, int *count)
{
    int i, j, pos, temp;
    for (i = 0; i < n - 1; i++)
    {
        pos = i;
        for (j = i + 1; j < n; j++)
        {
            (*count)++;
            if (a[j] < a[pos])
                pos = j;
        }
        if (i != pos)
        {
            temp = a[i];
            a[i] = a[pos];
            a[pos] = temp;
        }
    }
}

int main()
{
    int *a, n, i, count = 0;
    printf("Enter the value of n: ");
    scanf("%d", &n);
    a = (int*)malloc(n * sizeof(int));
    
    srand(time(NULL));

    for (i = 0; i < n; i++)
        a[i] = rand() % 100;

    selection_sort(a, n, &count);

    printf("Sorted elements are:\n");
    for (i = 0; i < n; i++)
        printf("%d\t", a[i]);

    printf("\nBasic operation count = %d\n", count);
    free(a);
    return 0;
}


//QUICK SORT
_____________________________________

#include <stdio.h>
#include <stdlib.h>
#include <time.h>

static int count = 0;

int partition(int a[], int l, int r)
{
    int pivot = a[l], i = l, j = r + 1, temp;
    do
    {
        do
        {
            i++;
            count++;
        } while (i <= r && a[i] < pivot);

        do
        {
            j--;
            count++;
        } while (j > l && a[j] > pivot);

        if (i < j)
        {
            temp = a[i];
            a[i] = a[j];
            a[j] = temp;
        }
    } while (i < j);

    temp = a[l];
    a[l] = a[j];
    a[j] = temp;

    return j;
}

void quicksort(int a[], int l, int r)
{
    if (l < r)
    {
        int s = partition(a, l, r);
        quicksort(a, l, s - 1);
        quicksort(a, s + 1, r);
    }
}

int main()
{
    int n, *a;
    printf("Enter the value of N: ");
    scanf("%d", &n);

    a = (int *)malloc(n * sizeof(int));

    srand(time(NULL));

    printf("Input elements are:\n");
    for (int i = 0; i < n; i++)
    {
        a[i] = rand() % 10001;
        printf("%d\t", a[i]);
    }

    quicksort(a, 0, n - 1);

    printf("\nSorted elements are:\n");
    for (int i = 0; i < n; i++)
    {
        printf("%d\n", a[i]);
    }

    printf("Basic operation count = %d\n", count);

    free(a);
    return 0;
}



//MERGE SORT
________________________

#include <stdio.h>
#include <stdlib.h>
#include <math.h>

static int count = 0;

void merge(int a[], int b[], int p, int c[], int q)
{
    int i = 0, j = 0, k = 0;
    while (i < p && j < q)
    {
        count++;
        if (b[i] <= c[j])
            a[k++] = b[i++];
        else
            a[k++] = c[j++];
    }
    while (i < p)
        a[k++] = b[i++];
    while (j < q)
        a[k++] = c[j++];
}

void mergesort(int a[], int n)
{
    if (n > 1)
    {
        int p = n / 2;
        int q = n - p;
        int *b = (int *)malloc(p * sizeof(int));
        int *c = (int *)malloc(q * sizeof(int));
        int i, j = 0;

        for (i = 0; i < p; i++)
            b[i] = a[i];
        for (i = p; i < n; i++)
            c[j++] = a[i];

        mergesort(b, p);
        mergesort(c, q);
        merge(a, b, p, c, q);

        free(b);
        free(c);
    }
}

int main()
{
    int i, n, *a;
    printf("Enter the number of elements: ");
    scanf("%d", &n);
    a = (int *)malloc(n * sizeof(int));
    printf("Array elements are:\n");
    for (i = 0; i < n; i++)
    {
        a[i] = rand() % 10001;
        printf("%d\t", a[i]);
    }
    mergesort(a, n);
    printf("\nThe sorted array elements are:\n");
    for (i = 0; i < n; i++)
    {
        printf("%d\n", a[i]);
    }
    printf("Basic operation count = %d\n", count);
    free(a);
    return 0;
}




//PRIMS ALGO
________________________________

#include <stdio.h>
#include <stdlib.h>
#include <limits.h> // for INT_MAX

void prims(int n, int s, int cost[][10])
{
    int i, j, a, b, min, totalcost = 0, ecounter = 0;
    int tvertex[10] = {0};
    tvertex[s] = 1;

    while (ecounter < n - 1)
    {
        min = INT_MAX;
        for (i = 0; i < n; i++)
        {
            if (tvertex[i] == 1)
            {
                for (j = 0; j < n; j++)
                {
                    if (tvertex[j] == 0 && cost[i][j] < min && cost[i][j] != 0)
                    {
                        min = cost[i][j];
                        a = i;
                        b = j;
                    }
                }
            }
        }
        printf("Edge from vertex %d to %d is %d\n", a, b, min);
        tvertex[b] = 1;
        totalcost += min;
        ecounter++;
    }
    printf("mincost = %d\n", totalcost);
}

int main()
{
    int n, s;
    int cost[10][10];

    printf("Enter the number of vertices: ");
    scanf("%d", &n);
    
    printf("Enter the cost matrix:\n");
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
        {
            scanf("%d", &cost[i][j]);
        }
    }

    printf("Enter the starting vertex: ");
    scanf("%d", &s);

    prims(n, s, cost);

    return 0;
}
