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



