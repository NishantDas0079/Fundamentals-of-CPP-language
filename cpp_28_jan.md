# Reading and Displaying elements of an 1-D array

```cpp
#include <iostream>
using namespace std;

int main()
{
    int a[5]={1,4,6,9,10};
    for (int i=0;i<5;i++){
        cout << a[i] << endl;
    }
    return 0;
}
```

# Finding sum of elements in an 1-D array

```cpp
#include <iostream>
using namespace std;
int main()
{
    int array[5]={3,5,7,11,22};
    int sum=0;
    for (int i=0;i<5;i++){
        sum+=array[i];
    }
    cout << "sum of all elements:-" << endl;
    return 0;
}
```

# Copy one array into another array

```cpp
#include <iostream>
using namespace std;

int main()
{
    int a[5] = {1, 2, 3, 4, 5};
    int b[5];

    for (int i = 0; i < 5; i++) {
        b[i] = a[i];
    }

    // Print copied array
    for (int i = 0; i < 5; i++) {
        cout << b[i] << " ";
    }

    return 0;
}
```

# Print array elements at even index positions

```cpp
#include <iostream>
using namespace std;

int main() {
    int n;
    cout << "Enter number of elements: ";
    cin >> n;

    int arr[n];
    cout << "Enter elements:\n";
    for (int i = 0; i < n; i++) {
        cin >> arr[i];
    }

    cout << "Elements at even index positions:\n";
    for (int i = 0; i < n; i += 2) {
        cout << arr[i] << " ";
    }

    return 0;
}
```

# Read and display a 2D array (Row wise) 

```cpp
#include <iostream>
using namespace std;

int main() {
    int r, c;
    cout << "Enter rows and columns: ";
    cin >> r >> c;

    int mat[r][c];
    cout << "Enter matrix elements:\n";
    for (int i = 0; i < r; i++) {
        for (int j = 0; j < c; j++) {
            cin >> mat[i][j];
        }
    }

    cout << "Matrix is:\n";
    for (int i = 0; i < r; i++) {
        for (int j = 0; j < c; j++) {
            cout << mat[i][j] << " ";
        }
        cout << endl;
    }

    return 0;
}
```



