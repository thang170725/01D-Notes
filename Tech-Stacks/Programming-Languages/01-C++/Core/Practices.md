## test tràn ghi đè bộ nhớ
```c++
#include <iostream>
using namespace std;

int main(){
    char a[3];
    a[100] = 'a';
    return 0;
}
```