# 1. Sum of first n natural numbers (command line)

```cpp
#include <iostream>
using namespace std;

int main(int argc, char *argv[])
{
    int n, sum = 0;

    if (argc > 1)
        n = atoi(argv[1]);
    else {
        cout << "Enter n: ";
        cin >> n;
    }

    for (int i = 1; i <= n; i++)
        sum += i;

    cout << "Sum = " << sum;
    return 0;
}
```

# 2. Remove duplicates from array

```cpp
#include <iostream>
using namespace std;

int main()
{
    int n, a[20];

    cout << "Enter size: ";
    cin >> n;

    for (int i = 0; i < n; i++)
        cin >> a[i];

    for (int i = 0; i < n; i++)
        for (int j = i + 1; j < n; j++)
            if (a[i] == a[j]) {
                for (int k = j; k < n - 1; k++)
                    a[k] = a[k + 1];
                n--;
                j--;
            }

    cout << "Result: ";
    for (int i = 0; i < n; i++)
        cout << a[i] << " ";
}
```

# 3. Count alphabets (command line input)

```cpp
#include <iostream>
using namespace std;

int main(int argc, char *argv[])
{
    int count[26] = {0};

    for (int i = 1; i < argc; i++)
        for (int j = 0; argv[i][j]; j++)
            if (argv[i][j] >= 'a' && argv[i][j] <= 'z')
                count[argv[i][j] - 'a']++;
            else if (argv[i][j] >= 'A' && argv[i][j] <= 'Z')
                count[argv[i][j] - 'A']++;

    for (int i = 0; i < 26; i++)
        if (count[i] > 0)
            cout << char(i + 'A') << " : " << count[i] << endl;

    return 0;
}
```

# 4. Menu-driven String Operations (no inbuilt functions)

```cpp
#include <iostream>
using namespace std;

int length(char s[])
{
    int i = 0;
    while (s[i] != '\0') i++;
    return i;
}

int main()
{
    char s1[50], s2[50];
    int ch;

    cout << "Enter string 1: ";
    cin.getline(s1, 50);
    cout << "Enter string 2: ";
    cin.getline(s2, 50);

    do {
        cout << "\n1.Address\n2.Concat\n3.Compare\n4.Length\n5.Lower to Upper\n6.Reverse\n0.Exit\n";
        cin >> ch;

        if (ch == 1)
            for (int i = 0; s1[i]; i++)
                cout << (void*)&s1[i] << endl;

        if (ch == 2) {
            int i = length(s1), j = 0;
            while (s2[j])
                s1[i++] = s2[j++];
            s1[i] = '\0';
            cout << s1;
        }

        if (ch == 3) {
            int i = 0;
            while (s1[i] && s2[i] && s1[i] == s2[i]) i++;
            cout << s1[i] - s2[i];
        }

        if (ch == 4)
            cout << length(s1);

        if (ch == 5) {
            for (int i = 0; s1[i]; i++)
                if (s1[i] >= 'a' && s1[i] <= 'z')
                    s1[i] -= 32;
            cout << s1;
        }

        if (ch == 6) {
            for (int i = length(s1) - 1; i >= 0; i--)
                cout << s1[i];
        }

    } while (ch != 0);

    return 0;
}
```

# 5. Merge two sorted arrays

```cpp
#include <iostream>
using namespace std;

int main()
{
    int a[5]={1,3,5,7,9}, b[5]={2,4,6,8,10};
    int c[10], i=0, j=0, k=0;

    while (i<5 && j<5)
        c[k++] = (a[i]<b[j]) ? a[i++] : b[j++];

    while (i<5) c[k++] = a[i++];
    while (j<5) c[k++] = b[j++];

    for (i=0;i<10;i++)
        cout<<c[i]<<" ";
}
```

# 6. Binary Search

Recursive
```cpp
int bin(int a[], int l, int r, int x)
{
    if (l > r) return -1;
    int m = (l + r) / 2;
    if (a[m] == x) return m;
    if (x < a[m]) return bin(a, l, m - 1, x);
    return bin(a, m + 1, r, x);
}
```

Non-Recursive
```cpp
int bin(int a[], int n, int x)
{
    int l=0,r=n-1;
    while(l<=r){
        int m=(l+r)/2;
        if(a[m]==x) return m;
        if(x<a[m]) r=m-1;
        else l=m+1;
    }
    return -1;
}
```

# 7. GCD

Recursive
```cpp
int gcd(int a,int b)
{
    if(b==0) return a;
    return gcd(b,a%b);
}
```

Non-Recursive
```cpp
int gcd(int a,int b)
{
    while(b){
        int t=b;
        b=a%b;
        a=t;
    }
    return a;
}
```

# 8. Matrix (basic exception)

```cpp
#include <iostream>
using namespace std;

class Matrix {
public:
    int a[2][2];
    void read() {
        for(int i=0;i<2;i++)
            for(int j=0;j<2;j++)
                cin>>a[i][j];
    }
    void add(Matrix m) {
        for(int i=0;i<2;i++)
            for(int j=0;j<2;j++)
                cout<<a[i][j]+m.a[i][j]<<" ";
    }
};
```

# 9. Runtime Polymorphism

```cpp
#include <iostream>
using namespace std;

class Person {
public:
    virtual void display() {
        cout<<"Person\n";
    }
};

class Student: public Person {
public:
    void display() {
        cout<<"Student\n";
    }
};

class Employee: public Person {
public:
    void display() {
        cout<<"Employee\n";
    }
};
```

# 10. Triangle with validation

```cpp
class Triangle {
public:
    Triangle(int a,int b,int c){
        if(a<=0||b<=0||c<=0)
            cout<<"Invalid sides";
        else if(a+b<=c||a+c<=b||b+c<=a)
            cout<<"Not a triangle";
        else
            cout<<"Valid triangle";
    }
};
```

# 11. Student File Handling

```cpp
#include <fstream>
using namespace std;

class Student {
public:
    int roll;
    char name[20];
};

int main()
{
    Student s;
    ofstream out("data.txt");

    for(int i=0;i<5;i++){
        cin>>s.roll>>s.name;
        out.write((char*)&s,sizeof(s));
    }
    out.close();

    ifstream in("data.txt");
    while(in.read((char*)&s,sizeof(s)))
        cout<<s.roll<<" "<<s.name<<endl;
}
```

# 12. Copy file removing spaces

```cpp
#include <fstream>
using namespace std;

int main()
{
    char ch;
    ifstream in("a.txt");
    ofstream out("b.txt");

    while(in.get(ch))
        if(ch!=' ' && ch!='\n' && ch!='\t')
            out.put(ch);

    in.close();
    out.close();
}
```
