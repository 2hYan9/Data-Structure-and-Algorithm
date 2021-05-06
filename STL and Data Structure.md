### STL与数据结构

STL, Standard Template Library，标准模板库，是C++提供的一个抽象数据类型(Abstract Data Type, ADT)容器类，是各种常见的数据结构的容器类的模板。

#### vector类

vector翻译为向量，但是在实际使用中更可以将其看作是一个长度根据需要而自动改变的数组。

如果要使用vector类，则需要添加vector头文件，即`#include<vector>`除此之外，还需要声明名称空间std。

##### 声明vector类对象

声明一个vector类的对象，

`vector<typename> obj_name;`

上面的这个定义实际上相当于声明了一个一维数组`obj_name[SIZE]`，只不过其长度可以根据实际需要而变化，比较节省空间，也就是所谓的“变长数组”。

下面的语句将声明一个vector数组，

`vector<typename> array_name[array_size];`

需要注意的是，上面语句中声明的数组中的每个元素都是一个vector对象，相当于是一个二维的数组。

不过要注意与下面这种声明的区别：

`vector< vector<int> > name;`，这条语句的声明也相当于是声明一个二维数组，但是与上面的vector对象数组的声明不同的是，上面那样的声明已经将第一维声明为array_size，而这里的声明则没有限定。

##### 访问vector容器内的元素

通过下标访问，和访问普通的数组元素是一样的，这里的下标范围和数组也一样，是0\~size()-1

也可以通过迭代器访问，其定义是`vector<typename>::iterator it;`，可以将迭代器理解成一个类似指针的东西，下面给出一个vector迭代器使用的示例：

```c++
#include <iostream>
#include <vector>

int main() {
    using namespace std;
    vector<int> vi;
    for(int i = 1; i <= 5; i++){
        vi.push_back(i);
    }
    for(vector<int>::iterator it = vi.begin(); it != vi.end();it++){
        cout << *it << " ";
    }
    return 0;
}
```

上面个这段代码中，`vi.begin()`返回第一个元素的地址，然后用这个地址初始化一个迭代器`vector<int>::iterator it`，而`vi.end()`返回这个容器中最后一个元素的地址。

可以通过递增运算符`++`使迭代器容器中的下一个元素。

这里需要注意的是，vector容器的迭代器不支持`it < vi.end()`的写法，所以循环结构中的条件判断应该是`it != vi.end()`。

 此外，当容器是vector类时，可以通过`*(it + i)`的方式访问vector容器中的第i个元素：

```c++
#include <iostream>
#include <vector>

int main() {
    using namespace std;
    vector<int> vi;
    for(int i = 1; i <= 5; i++){
        vi.push_back(i);
    }
    vector<int>::iterator it = vi.begin();
    cout << *(it + 2);
    return 0;
}
```

##### 常用的方法

push_back()方法，接受一个模板参数类型的数据为参数，将其添加到vector容器的最后一个元素的位置。

其使用方法在上面的代码中已经演示过了。

pop_back()方法，删除容器对象中最后一个位置上的元素：

```C++
#include <iostream>
#include <vector>

int main() {
    using namespace std;
    vector<int> vi;
    for(int i = 1; i <= 5; i++){
        vi.push_back(i);
    }
    vi.pop_back();
    vector<int>::iterator it = vi.begin();
    while(it != vi.end()){
        cout << *it << " ";
        it++;
    }
    return 0;
}
```

size()方法，返回容器中存储元素的个数：

```c++
#include <iostream>
#include <vector>

int main() {
    using namespace std;
    vector<int> vi;
    for(int i = 1; i <= 5; i++){
        vi.push_back(i);
    }
    cout << vi.size();
    return 0;
}
```

clear()方法，用于清空容器中的所有元素，时间复杂度为`O(n)`：

```c++
#include <iostream>
#include <vector>

int main() {
    using namespace std;
    vector<int> vi;
    for(int i = 1; i <= 5; i++){
        vi.push_back(i);
    }
    vi.clear();
    cout << vi.size() << endl;
    return 0;
}
```

insert()方法，接受两个参数，第一个参数是一个迭代器，第二个参数是一个模板参数类型的变量，其功能是将这个变量的值插入到迭代器所指向的位置：

```c++
#include <iostream>
#include <vector>

int main() {
    using namespace std;
    vector<int> vi;
    for(int i = 1; i <= 5; i++){
        vi.push_back(i);
    }
    vector<int>::iterator it = vi.begin();
    vi.insert(it + 2, -1);
    while(it != vi.end()){
        cout << *it << " ";
        it++;
    }
    return 0;
}
```

erase()方法，有两个版本，第一个版本以一个迭代器为参数，删除迭代器所指向位置的元素：

```c++
#include <iostream>
#include <vector>

int main() {
    using namespace std;
    vector<int> vi;
    for(int i = 1; i <= 5; i++){
        vi.push_back(i);
    }
    vector<int>::iterator it = vi.begin();
    vi.erase(it + 3);
    while(it != vi.end()){
        cout << *it << " ";
        it++;
    }
    return 0;
}
```

第二个版本是以两个迭代器为参数，删除这两个迭代器所指向的位置之间的元素：

```c++
#include <iostream>
#include <vector>

int main() {
    using namespace std;
    vector<int> vi;
    for(int i = 1; i <= 5; i++){
        vi.push_back(i);
    }
    vector<int>::iterator it = vi.begin();
    vi.erase(it + 1, it + 3);   //erase vi[1], vi[2]
    while(it != vi.end()){
        cout << *it << " ";
        it++;
    }
    return 0;
}
```

所以如果要清空一个vector容器中的所有元素，`vi.clear()`和`vi.erase(vi.begin(), vi.end())`方法是等价的。

在一些元素个数不确定的场景下使用vector能够很好的节省空间。

#### set类

set翻译为集合，是一个内部自动有序且不含重复要算的容器。

如果要使用set，需要添加set头文件，即`#include <set>`，并且声明名称空间为std即可。

##### 声明set类对象

下面的语句用于声明一个存储typename类型的数据的set对象：

`set<typename> objname;`

这里的模板类型参数也可以是模板类。

声明一个set数组:

`set<typename> arrayName[arraySize];`

上面的语句声明一个数组，这个数组中的每个元素都是一个set类型的对象。

##### 访问set容器内的元素

set容器内的元素只能通过迭代器进行方法，并且set类的迭代器不再支持`*(it + i)`的方式访问第i个元素。

下面的代码演示了如何通过迭代器访问set类对象中的元素：

```C++
#include <iostream>
#include <set>

int main(){
    using namespace std;
    set<int> st;
    st.insert(3);
    st.insert(5);
    st.insert(2);
    st.insert(3);
    for(set<int>::iterator it = st.begin(); it != st.end(); it++){
        cout << *it << " ";
    }
    return 0;
}
```

这里set类型的迭代器的声明方法和vector类型的迭代器的声明方法一样，并且需要注意的是set类型的迭代器同样不支持`it < st.end();`判断语句，所以循环结构中的条件判断语句应该是`it != st.end();`。

上面这段代码的输出结果为：`2 3 5`。

可以发现，这里不仅自动去除了重复的元素，并且还自动对其中的元素进行了排序。

##### 常用的方法

insert()方法，接受一个模板参数类型的变量作为参数，然后将这个元素插入到容器中合适的位置：

```c++
#include <iostream>
#include <set>

int main(){
    using namespace std;
    set<int> st;
    st.insert(3);
    st.insert(5);
    st.insert(2);
    st.insert(3);
    for(set<int>::iterator it = st.begin(); it != st.end(); it++){
        cout << *it << " ";
    }
    return 0;
}
```

set类中的insert()方法的时间复杂度为`O(logN)`，其中N为容器内元素个数。

find()方法，接受一个模板参数类型的变量作为参数，然后返回一个指向这个参数位置的迭代器，时间复杂度为`O(logN)`，其中N为容器内元素的个数：

```c++
v#include <iostream>
#include <set>

int main(){
    using namespace std;
    set<int> st;
    for(int i = 1; i <= 5; i++) st.insert(i);
    set<int>::iterator it = st.find(2);
    cout << *it << endl;
    return 0;
}
```

erase()方法，set类中的erase()方法同样有两种版本，第一种版本接受一个迭代器作为参数，然后删除这个迭代器所指向位置的元素：

```c++
#include <iostream>
#include <set>

int main(){
    using namespace std;
    set<int> st;
    for(int i = 1; i <= 5; i++) st.insert(i);
    set<int>::iterator it = st.find(2);
    st.erase(it);
    for(it = st.begin(); it != st.end(); it++) cout << *it << " ";
    return 0;
}
```

第二种版本接受两个迭代器为参数，然后删除这两个迭代器所指向的位置之间的元素：

```c++
#include <iostream>
#include <set>

int main(){
    using namespace std;
    set<int> st;
    for(int i = 1; i <= 5; i++) st.insert(i);
    set<int>::iterator it = st.find(3);
    st.erase(it, st.end());
    for(it = st.begin(); it != st.end(); it++) cout << *it << " ";
    return 0;
}
```

size()方法，用于返回容器内元素的个数，时间复杂度为`O(1)`：

```c++
#include <iostream>
#include <set>

int main(){
    using namespace std;
    set<int> st;
    for(int i = 1; i <= 5; i++) st.insert(i);
    cout << st.size();
    return 0;
}
```

clear()方法，用于情况容器内的所有元素，时间复杂度为`O(N)`：

```c++
#include <iostream>
#include <set>

int main(){
    using namespace std;
    set<int> st;
    for(int i = 1; i <= 5; i++) st.insert(i);
    st.clear();
    cout << st.size();
    return 0;
}
```

set类容器的主要作用是自动去重并自动按升序排序。

#### string类

在C++中，通常将使用字符数组存储的字符串称为C风格字符串(C-style string)，而为了更方便的处理字符串数据，C++的STL中定义了一个用于处理字符串数据的类string。

如果要使用string类，那么需要在头文件中添加string头文件，即`#include<string>`，并且声明名称空间为std。

##### 声明string类对象

声明一个string类对象的语句如下：

`string var_name;`

和前面介绍的几种STL类不同，声明一个string类的对象时不需要添加类型参数。

声明一个string类对象时，可以使用字符常量对其进行初始化：

`string str = "abcd";`

##### 访问string类对象中的字符

如果使用string类对象存储字符串数据，那么如果要访问这个字符串中的某一个字符，可以通过下标的方式进行访问：

```c++
#include <iostream>
#include <string>

int main(){
    using namespace std;
	string str = "abcd";
	for(int i = 0; i < str.length(); i++)
		cout << str[i] << " ";
	return 0;
}
```

也可以使用迭代器访问string类对象存储的字符串中的某一个字符：

```c++
#include <iostream>
#include <string>

int main(){
    using namespace std;
    string str = "abcd";
    for(string::iterator it = str.begin(); it != str.end(); it++)
        cout << *it << " ";
    cout << *(str.begin() + 2);
    return 0;
}
```

这里需要注意的是，string类对象和vector对象一样可以通过迭代器加一个整数的方式访问字符串中的某个字符。

##### 常用的方法

可以使用cin来读取一个字符串，也可以使用cout输出一个字符串，再输入输出这方面，string类的对象和一般的C风格字符串的使用是一样的：

```c++
#include <iostream>
#include <string>

int main(){
    using namespace std;
	string str;
	cin >> str;
	cout << str;
	return 0;
}
```

但是如果要使用pringf()函数来输出一个string类的对象，那么可以借助string类对象的一个成员函数c_str()函数进行输出：

```c++
#include <iostream>
#include <string>
#include <stdio.h>

int main(){
    using namespace std;
    string str = "abcd";
    printf("%s\n", str.c_str());
    return 0;
}
```

operator+=()方法，可以将两个字符串拼接起来：

```c++
#include <iostream>
#include <string>

int main(){
    using namespace std;
    string str1 = "abc", str2 = "xyz", str3;
    str3 = str1 + str2;
    str1 += str2;
    cout << str1 << endl;
    cout << str3 << endl;
    return 0;
}
```

这个运算符对字符数组和char类型的变量也同样适用：

```C++
#include <iostream>
#include <string>

int main(){
    using namespace std;
    string word;
    char w[5] = "abcd";
    for(int i = 0; i < 5; i++)
        word += w[i];
    cout << word << endl;
    word += w;
    cout << word << endl;
    return 0;
}
```

operator>()方法，可以直接使用比较运算符来比较两个字符串的字典顺序：

```c++
#include <iostream>
#include <string>

int main(){
    using namespace std;
    string str1 = "abc", str2 = "xyz", str3 = "aa", str4 = "aaa";
    if(str3 < str4) cout << '\"' << str3 << "\" < \"" << str4 << '\"' << endl;
    if(str1 != str3) cout << '\"' << str1 << "\" != \"" << str3 << '\"' << endl;
    if(str2 >= str1) cout << '\"' << str2 << "\" >= \"" << str1 << '\"' << endl;
    return 0;
}
```

length()\size()方法，返回字符串的长度，时间复杂度为`O(1)`：

```C++
#include <iostream>
#include <string>

int main(){
    using namespace std;
    string str = "abcd";
    cout << str.size() << " " << str.length() << endl;
    return 0;
}
```

insert()方法，string类的insert()方法有两个版本，第一个版本接受两个参数，第一个参数是一个整数，用于表示插入的位置，第二参数是一个字符串，为待插入的字符串：

```c++
#include <iostream>
#include <string>

int main(){
    using namespace std;
    string str1 = "abcxyz", str2 = "opq";
    str1.insert(3, str2);
    cout << str1 << endl;
    return 0;
}
```

insert()方法的另一个版本是接受三个参数，第一个参数为指向待插入位置的迭代器，第二三个参数分别为指向待插入子字符串首位的迭代器：

```c++
#include <iostream>
#include <string>

int main(){
    using namespace std;
    string str1 = "abcxyz", str2 = "opq";
    str1.insert(str1.begin() + 3, str2.begin(), str2.end());
    cout << str1 << endl;
    return 0;
}
```

erase()方法，string类的erase()方法有三个版本，第一个版本只接受一个参数，这个参数为指向待删除字符位置的迭代器：

```c++
#include <iostream>
#include <string>

int main(){
    using namespace std;
    string str = "abcdefg";
    str.erase(str.begin() + 4);
    cout << str << endl;
    return 0;
}
```

erase()方法的第二版本接受两个参数，分别为指向待删除区间的起始位置的迭代器和结束位置的迭代器：

```c++
#include <iostream>
#include <string>

int main(){
    using namespace std;
    string str = "abcdefg";
    str.erase(str.begin() + 2, str.end() - 1);
    cout << str << endl;
    return 0;
}
```

erase()方法的第三个版本以两个整数作为参数，第一个参数用于表示需要删除的第一个字符的位置，第二个参数用于表示待删除字符的个数：

```c++
#include <iostream>
#include <string>

int main(){
    using namespace std;
    string str = "abcdefg";
    str.erase(3, 2);
    cout << str << endl;
    return 0;
}
```

clear()方法，删除对象中存储的字符串数据，时间复杂度为`O(1)`:

```c++
#include <iostream>
#include <string>

int main(){
    using namespace std;
    string str = "abcdefg";
    str.clear();
    cout << str.size() << endl;
    return 0;
}
```

substr()方法，接受两个整数为参数，第一个整数用于指出子字符串起始的为，第二个字符串用于指出子字符串的长度：

```C++
#include <iostream>
#include <string>

int main(){
    using namespace std;
    string str = "abcd";
    cout << str.substr(1, 2);
    return 0;
}
```
find()方法，这个方法有两个版本，第一个版本是接受一个字符串为参数，如果这个参数是一个子字符串，则返回这个子字符串首次出现的位置，否则返回string::npos。第二个版本接受两个参数，第一个参数是带查找的子字符串，第二个参数是一个整数，从这个整数表示的位置开始查找：

```c++
#include <iostream>
#include <string>

int main(){
    using namespace std;
    string str = "Thank you for your smile.";
    string str2 = "you";
    string str3 = "me";
    if(str.find(str2) != string::npos)
        cout << str.find(str2) << endl;
    if(str.find(str2, 7) != string::npos)
        cout << str.find(str2, 7) << endl;
    if(str.find(str3) != string::npos)
        cout << str.find(str3) << endl;
    else
        cout << "I know there is no position for me." << endl;
    return 0;
}
```

replace()方法，这个方法也有两个版本，第一个版本接受三个参数，第一二个参数为整数，表示需要替换的起止位置号和需要替换的长度，第三个参数为用于替换的字符串；第二个版本接受三个参数，前两个参数为迭代器分别指向需要替换区间的起始位置和结束位置，第三个参数为用于替换的字符串：

```c++
#include <iostream>
#include <string>

int main(){
    using namespace std;
    string str = "Maybe you will turn around";
    string str2 = "will not";
    string str3 = "surely";
    cout << str.replace(10, 4, str2) << endl;
    cout << str.replace(str.begin(), str.begin() + 5, str3) << endl;
    return 0;
}
```

#### map类

C++中的map类对象类似于PHP中的关联数组，可以通过自定义数组索引值(key, 键值)创建数组。

map翻译为“映射”，可以将一般的数组理解成从int类型到另一种类型的映射，int类型的数组为int到int的映射，double类型的数组为int到double类型的映射。如果想要定义一个不是以int为原像的映射的话，那么可以使用map类对象。

如果要使用map类，需要在头文件中添加map头文件，即`#include <map>`，并且声明名称空间为std。

##### 声明map类对象

定义一个map类对象的通用格式如下：

*map<typename1, typename2> mp*

表示这是一个从typename1映射到typename2的一个映射，也就是说上面的语句中typename1是键的类型，typename2是值的类型。

需要注意的是，如果要定义一个以字符串为原像类型的映射，那么就必须使用string类，而不能使用char数组。

`map<string, int> mp;`

##### 访问map容器内的元素

正如前面所说，C++中的map类对象和PHP中的关联数组相似，如果要访问map类对象中的某一个元素，那么需要通过键值对的形式进行访问，比如定义一个从char映射到int类型的映射：`map<char, int> mp;`，如果要访问键为'c'的值，就通过`mp['c']`的形式进行访问。即通过关联数组的下标进行访问：

```c++
#include <iostream>
#include <map>

int main(){
    using namespace std;
    map<char, int> mp;
    mp['c'] = 20;
    mp['d'] = 25;
    mp['c'] = 30;		//rewrite mp['c']
    cout << mp['c'] << endl;
    cout << mp['d'] << endl;
    return 0;
}
```

需要注意的是，map类对象中的键是唯一的。

对于map类对象，也可以通过迭代器来访问map类对象中的数据。正如前面所说，迭代器实际上就是模板类型参数的指针，而在这里可以将map的模板参数视为一个结构体，这个结构体的第一个成员为first，第二个成员为second，分别对应原像与像：

```c++
#include <iostream>
#include <map>

int main(){
    using namespace std;
    map<char, int> mp;
    mp['m'] = 20;
    mp['r'] = 30;
    mp['a'] = 40;
    for(map<char, int>::iterator it = mp.begin(); it != mp.end(); it++)
        cout << it -> first << " " << it -> second << endl;
    return 0;
}
```

上面这段代码的输出为：

```
a 40
m 20
r 30
```

可以发现，mp对象对这些数据根据键的大小自动按升序进行了排序。

##### 常用的方法

find()方法，以一个键类型的数值作为参数，然后返回指向这个键的迭代器：

```c++
#include <iostream>
#include <map>

int main(){
    using namespace std;
    map<char, int> mp;
    mp['a'] = 20;
    mp['b'] = 30;
    mp['c'] = 40;
    map<char, int>::iterator it = mp.find('b');
    cout << it -> first << " " << it -> second << endl;
    return 0;
}
```

erase()方法，这个方法有多个版本，第一个版本是接受一个迭代器为参数，然后删除这个迭代器所指向的位置的元素：

```c++
#include <iostream>
#include <map>

int main(){
    using namespace std;
    map<char, int> mp;
    mp['a'] = 20;
    mp['b'] = 30;
    mp['c'] = 40;
    map<char, int>::iterator it = mp.find('b');
    mp.erase(it);
    for(map<char, int>::iterator i = mp.begin(); i != mp.end(); i++) cout << i -> first << " " << i -> second << endl;
    return 0;
}
```

第二个版本是接受一个原像类型的数值作为参数，然后删除这个数值对应的键值对：

```c++
#include <iostream>
#include <map>

int main(){
    using namespace std;
    map<char, int> mp;
    mp['a'] = 20;
    mp['b'] = 30;
    mp['c'] = 40;
    mp.erase('b');
    for(map<char, int>::iterator i = mp.begin(); i != mp.end(); i++) cout << i -> first << " " << i -> second << endl;
    return 0;
}
```

第三个版本接受两个参数，这两个参数分别为指向待删除区间起止位置的迭代器和待删除区间结束位置的迭代器：

```c++
#include <iostream>
#include <map>

int main(){
    using namespace std;
    map<char, int> mp;
    mp['a'] = 20;
    mp['b'] = 30;
    mp['c'] = 40;
    map<char, int>::iterator it = mp.find('b');
    mp.erase(it, mp.end());
    for(map<char, int>::iterator i = mp.begin(); i != mp.end(); i++) cout << i -> first << " " << i -> second << endl;
    return 0;
}
```

size()方法，返回map中的键值对个数：

```c++
#include <iostream>
#include <map>

int main(){
    using namespace std;
    map<char, int> mp;
    mp['a'] = 20;
    mp['b'] = 30;
    mp['c'] = 40;
    cout << mp.size() << endl;
    return 0;
}
```

clear()方法，清空对象中存储的数据：

```c++
#include <iostream>
#include <map>

int main(){
    using namespace std;
    map<char, int> mp;
    mp['a'] = 20;
    mp['b'] = 30;
    mp['c'] = 40;
    mp.clear();
    cout << mp.size() << endl;
    return 0;
}
```

C++11中新添加了unordered_map类，使其可以不对数据进行排序，从而节省了大量时间。

#### queue类

queue是一种实现“先进先出”概念的经典数据结构。

如果要使用queue，那么需要在头文件中添加queue文件，即`#include<queue>`，并且声明名称空间为std。

##### 声明queue类对象

和其他STL模板类一样，声明queue类对象的语句通用格式为：

`queue<typename> name;`

##### 访问queue类对象中的元素

由于队列(queue)本身就是一种“先进先出”的限制性数据结构，所以只能通过front()方法来访问队列中的第一个元素，而通过方法back()方法访问队列中的最后一个元素：

```c++
#include <iostream>
#include <queue>

int main(){
    using namespace std;
    queue<int> q;
    for(int i = 1; i <= 5; i++)
        q.push(i);
    cout << q.front() << " " << q.back() << endl;
    return 0;
}
```

##### 常用的方法

push()方法，接受一个类型参数中的类型的数据，将这个数据放入队列。时间复杂度为`O(1)`

pop()方法，将位于队列中的第一个元素拿出队列，没有参数和返回值，时间复杂度是`O(1)`：

```c++
#include <iostream>
#include <queue>

int main(){
    using namespace std;
    queue<int> q;
    for(int i = 1; i <= 5; i++)
        q.push(i);
   for(int i = 1; i <= 3; i++){
        cout << q.front() << " ";
        q.pop();
   }
    return 0;
}
```

size()方法，返回队列中元素个数：

```c++
#include <iostream>
#include <queue>

int main(){
    using namespace std;
    queue<int> q;
    for(int i = 1; i <= 5; i++)
        q.push(i);
    cout << q.size() << endl;
    return 0;
}
```

empty()方法，判断队列是否为空，如果是空的，则返回true，否则返回false，时间复杂度为`O(1)`：

```c++
#include <iostream>
#include <queue>

int main(){
    using namespace std;
    queue<int> q;
    for(int i = 1; i <= 5; i++)
        q.push(i);
    cout << q.size() << endl;
    while(!q.empty()) q.pop();
    cout << q.size() << endl;
    return 0;
}
```

队列用于实现广度优先搜索算法。

除了一般的queue类外，还有一种双端队列deque，这种队列首尾都可以进行插入和删除操作；还有另一种队列priority_queue队列，这种队列是通过堆实现的默认将当前最大元素放在队首的一种队列。

#### stack类

stack翻译为“栈”，是一种经典的“先进后出”的数据结构。

如果要使用stack类，那么要在头文件中添加stack头文件，并且声明名称为std。

##### 声明stack类对象

和其他的STL模板类的声明语句一样，下面的语句可以用于声明一个stack类的对象：

`stack<typename> name;`

##### 访问stack容器内的元素

因为stack本身就是一种具有“先进后出”限制的数据结构，所以只能通过top()成员函数来访问栈顶的元素：

```c++
#include <iostream>
#include <stack>

int main(){
    using namespace std;
    stack<int> s;
    for(int i = 1; i <= 5; i++)
        s.push(i);
    cout << s.top() << endl;
    return 0;
}
```

##### 常用的方法

push()方法，接受一个类型参数类型的数据为参数，然后将这个数据压入栈中，时间复杂度为`O(1)`：

top()方法，访问栈顶的元素，时间复杂度为`O(1)`：

```c++
#include <iostream>
#include <stack>

int main(){
    using namespace std;
    stack<int> s;
    for(int i = 1; i <= 5; i++)
        s.push(i);
    cout << s.top() << endl;
    return 0;
}
```

pop()方法，用于弹出栈顶元素，时间复杂度为`O(1)`：

```c++
#include <iostream>
#include <stack>

int main(){
    using namespace std;
    stack<int> s;
    for(int i = 1; i <= 5; i++)
        s.push(i);
    s.pop();
    cout << s.top() << endl;
    return 0;
}
```

size()方法，用于返回stack类对象中的元素个数，时间复杂度为`O(1)`：

```c++
#include <iostream>
#include <stack>

int main(){
    using namespace std;
    stack<int> s;
    for(int i = 1; i <= 5; i++)
        s.push(i);
    cout << s.size() << endl;
    return 0;
}
```

empty()方法，用于检测stack类对象是否为空，如果为空则返回true，否则返回false，时间复杂度为`O(1)`：

```c++
#include <iostream>
#include <stack>

int main(){
    using namespace std;
    stack<int> s;
    for(int i = 1; i <= 5; i++)
        s.push(i);
    cout << s.size() << endl;
    while(!s.empty()) s.pop();
    cout << s.size() << endl;
    return 0;
}
```

stack通常用于模拟实现一些递归，防止程序对栈内存的限制而导致程序运行出错。

#### 栈和队列的应用

 一个简单的计算器：给定一个非负整数的中缀表达式，计算这个表达式的值

这个问题的解决方法是先将给出的中缀表达式转换称为后缀表达式，然后再让程序计算这个后缀表达式的值，这是因为程序处理后缀表达式比处理中缀表达式要方便很多。

而将一个中缀表达式准换成为后缀表达式的方法如下：

1. 创建一个栈，这个栈用于存储操作符
2. 再创建一个队列，这个队列用于存储后缀表达式
3. 然后从左至右遍历给出的中缀表达式，执行这样的操作：
4. 如果为数字，则直接添加到队列中；
5. 如果是操作符，则将这个操作符与当前栈顶的操作符进行一个比较，如果当前的操作符比栈顶的操作符优先级高，则将这个操作符压入栈中；如果当前的操作符的优先级小于或者等于栈顶操作符的优先级，则将栈顶的操作符弹出并加入队列中；重复这样的操作直到当前运算符优先级大于栈顶操作符的优先级，然后再将当前操作符压入栈中。

在完成一次遍历后，队列中将存储原表达式的后缀表达式形式，然后让程序执行后缀表达式的计算即可完成运算。

程序计算中缀表达式的方法如下：

1. 创建一个栈
2. 从左至右遍历这个中缀表达式，执行这样的操作：
3. 如果是操作数，直接压入栈中
4. 如果是运算符，则从栈中弹出两个操作数执行运算，并将运算的结果压入栈中
5. 在中缀表达式合法的情况下，最终栈中只存在一个数字，就是这个中缀表达式的运算结果

所以代码实现如下：

```C++
#include <iostream>
#include <stack>
#include <queue>
#include <string>

//compare the precedence of two operators
bool opcmp(char a, char b){
    if(b == '*' || b== '/')
        return false;
    else{
        if(a == '*' || a == '/')
            return true;
        else
            return false;
    }
}

int main(){
    using namespace std;
    string infix;
    queue<string> suffix;
    stack<char> op;
    stack<double> result;
    cin >> infix;
    int i = 0;
    //generate the suffix
    while(i < infix.size()){
        if(infix[i] >= '0' && infix[i] <= '9'){
            string word;
            int j;
            for(j = i; infix[j] >= '0' && infix[j] <= '9'; j++) word += infix[j];
            suffix.push(word);
            i = j;
        }else{
            if(op.empty())
                op.push(infix[i]);
            else{
                bool flag = true;
                while(!op.empty()){
                    if(opcmp(infix[i], op.top())){
                        flag = false;
                        op.push(infix[i]);
                        break;
                    }
                    else{
                        string word;
                        word += op.top();
                        suffix.push(word);
                        op.pop();
                    }
                }
                if(flag) op.push(infix[i]);
            }
            i++;
        }
    }
    string w;
    w += op.top();
    suffix.push(w);
    //computer the result of suffix
    while(!suffix.empty()){
        string word = suffix.front();
        suffix.pop();
        if(word[0] >= '1' && word[0] <= '9'){
            double sum = 0;
            int pow = 1;
            for(int i = 0; i < word.size(); i++){
                int num = word[i] - '0';
                sum = sum * 10 + num;
            }
            result.push(sum);
        }else{
            double a = result.top();
            result.pop();
            double b = result.top();
            result.pop();
            double r;
            if(word[0] == '+') r = a + b;
            if(word[0] == '-') r = b - a;
            if(word[0] == '/') r = b / a;
            if(word[0] == '*') r = a * b;
            result.push(r);
        }
    }
    cout << result.top();
    return 0;
}
```

#### 链表的处理

线性表是一种比较常见的数据结构，可以将其看成是整数集到另一个集合的映射。线性表有两种实现，第一种称为顺序表，就是普通的数组；另一种就是这里要说的链表。

按正常方式（无论是静态内存还是动态内存）定义一个数组时，程序一般会分配一块连续的地址，这就是为什么能对指向数组的指针通过加整数的方式访问数组对应下标元素的原因；

而链表在内存中分配的为并不是连续的，而链表的两个节点之间通过一个指针来从一个节点指向另一个节点，所以链表的每个节点由两部分组成：数据域和指针域。

##### 动态内存分配

先看看两种动态内存分配的方式：

1. C语言中的malloc()函数和free()函数

   malloc()函数的使用方法：

   *typename \* p = (typename \*)malloc(sizeof(typename))*;

   例如：`int * p = (int *)malloc(sizeof(int));`

   该函数的功能是向内存申请一块大小为sizeof(typename)的空间，并且返回指向这块内存的指针，但是这个指针并没有类型，也就是说这是一个(void \*)类型的指针，所以此时需要将其强制转换称为等式左边的指针的类型，然后通过赋值运算符将这个地址赋给等式左边的指针内。

   malloc()函数创建动态数组：

   *typename \* p = (typename \*)malloc(arraysize \*  sizeof(typename))*

   例如：`int * p = (int *)malloc(10 * sizeof(int));  //int p[10];`

   malloc()函数在申请内存失败时会返回NULL

   free()函数的使用方法：

   *free(p)*

   例如：`free(p);`

   free()函数主要实现两个功能，先是释放指针p指向的内存空间，然后再将这个指针赋值为NULL。需要注意的是，free()并没有删除这个指针变量，而是将其存储的地址置为NULL。

2. C++中的new运算符和delete运算符

   new运算符的使用方法：

   *typename \* p = new typename*

   例如：`int * p = new int;`

    new运算符将一些原来需要程序员做的事情交给编译器处理，所以看起来比malloc()更加简洁。

   new运算符创建动态数组：

   *typename \* p = new typename [arraysize]*

   例如：`int * p = new int [10];`

   new运算符在申请内存失败时不会返回NULL，而是抛出一个异常。

   delete运算符的使用方法：

   *delete p*

   如果指针指向一个数组，那么使用方法为：

   *delete [] p*

> new运算符和malloc()函数的区别：
>
> `new/delete operator:`
>
> 1. 从一块被称为“自由存储区域(free store)”中申请内存，这块区域和堆内存之间的区别取决于具体的实现细节，当然new也可以通过定位new运算符从栈内存中申请内存，*typename \* p = new (BUF) typename*
> 2. 返回一个具有类型的指针
> 3. 申请内存失败时会抛出一个异常，而不是返回NULL
> 4. 由编译器自动计算申请内存的大小
> 5. 有一个专门用于处理数组的版本
> 6. 使用new运算符为指针重新分配内存的过程并不直观，需要先将指针原来指向的内存释放掉，然后再重新分配
> 7. 是否要调用malloc()和free()函数取决于具体的实现
> 8. new/delete运算符都可以被重载
> 9. 在对一个指向对象的指针使用new或者delete运算符或自动调用这个对象的构造函数和析构函数
>
> `malloc()/free() function:`
>
> 1. 从一块被称为“堆”的内存块中申请内存
> 2. 返回的(void \*)类型的指针
> 3. 申请内存失败是返回NULL
> 4. 申请内存时必须指明内存的大小，单位为字节
> 5. 如果要为了一个数组分配内存，那么需要手动计算内存的大小
> 6. 可以直接使用realloc()函数为一个指针重新分配内存
> 7. 不会调用new/delete运算符
> 8. malloc()和free()函数都不允许重载
> 9. 在对一个指向对象的指针使用malloc()或者free()函数时不会自动调用对象的构造函数和析构函数

##### 链表的基本操作

创建一个链表：

```C++
#include <iostream>

struct node{
    int data;
    node * next;
};

int main(){
    using namespace std;
    node * head = new node;
    node * p = head;
    int data[5];
    for(int i = 0; i < 5; i++){
        node * temp = new node;
        temp -> data = i + 1;
        temp -> next = nullptr;
        p -> next = temp;
        p = p -> next;
    }
    node * t = head -> next;
    while(t != nullptr){
        cout << t -> data << " ";
        t = t -> next;
    }
    return 0;
}
```

输出结果为：`1 2 3 4 5 `

上面这段代码创建一个链表，并且对其进行了遍历。需要注意的是头节点的数据域中并没有存储数据，所以遍历链表中的数据时，从`head -> next`开始遍历。

一般来说，new运算符和delete运算符是需要成对使用的，因为如果不及时释放掉申请的内存会造成内存泄露的问题，即内存占用过多，无法继续为新的指针申请内存。但是如果是代码量比较小的程序的话，可以不必使用delete释放申请的内存，因为程序结束时会自动回收为指针申请的内存。

查找元素：

```C++
#include <iostream>

struct node{
    int data;
    node * next;
};

int search(node * head, int obj){
    int count = 0;
    node * t = head -> next;
    while(t != nullptr){
        if(t -> data == obj) count++;
        t = t -> next;
    }
    return count;
}

int main(){
    using namespace std;
    node * head = new node;
    node * p = head;
    int data[5];
    for(int i = 0; i < 5; i++){
        node * temp = new node;
        temp -> data = i + 1;
        temp -> next = nullptr;
        p -> next = temp;
        p = p -> next;
    }
    cout << search(head, 2);
    return 0;
}
```

输出结果为：`1`

上面这段代码定义了一个用于查找链表元素的函数，不过这个函数只返回链表中目标数据的个数。

插入元素：

例如在上面创建的链表`1 -> 2 -> 3 -> 4 -> 5`的3和4之间插入一个2：

```C++
#include <iostream>

struct node{
    int data;
    node * next;
};

int main(){
    using namespace std;
    node * head = new node;
    node * p = head;
    int data[5];
    for(int i = 0; i < 5; i++){
        node * temp = new node;
        temp -> data = i + 1;
        temp -> next = nullptr;
        p -> next = temp;
        p = p -> next;
    }
    node * pre = head -> next;
    while(pre != nullptr){
        if(pre -> data == 3)
            break;
        pre = pre -> next;
    }
    node * current = new node;
    current -> data = 2;
    current -> next = pre -> next;
    pre -> next = current;
    node * t = head -> next;
    while(t != nullptr){
        cout << t -> data << " ";
        t = t -> next;
    }
    delete head;
    delete current;
    return 0;
}
```

输出结果为：`1 2 3 2 4 5 `

在插入元素时，需要保留前置节点的位置，这就意味着遍历链表时需要有两个指针。

删除元素：

还是上面的那个链表，如果要删除数据域为3的节点：

```C++
#include <iostream>

struct node{
    int data;
    node * next;
};

int main(){
    using namespace std;
    node * head = new node;
    node * p = head;
    int data[5];
    for(int i = 0; i < 5; i++){
        node * temp = new node;
        temp -> data = i + 1;
        temp -> next = nullptr;
        p -> next = temp;
        p = p -> next;
    }
    node * pre = head;
    p = head -> next;
    while(p != nullptr){
        if(p -> data == 3){
            pre -> next = p -> next;
            delete p;
        }else{
            pre = p;
            p = p -> next;
        }
    }
    node * t = head -> next;
    while(t != nullptr){
        cout << t -> data << " ";
        t = t -> next;
    }
    delete head;
    return 0;
}
```

输出结果为：`1 2 4 5`

在删除链表中的某个元素时，和插入元素的过程一样，需要保留前置节点的地址。

#### 树与二叉树

##### 树的概念

在数据结构中，树是用来概括某种传递关系的数据结构。为了简化，数据结构中把树枝分叉处、树叶、树根抽象成节点(node)，其中树根被抽象成根节点(root node)，对于一棵树来说最多存在一个根节点；把树叶抽象成叶子节点(leaf node)，且叶子节点不再延伸出新的节点。把茎干和树枝统一抽象成边(edge)，且一条边只用来连接两个节点。

一般把根节点放在最上方，然后向下延伸出若干条边到达子节点(child)，从而向下形成子树(subtree)，而子节点又向下延伸出边并连接一些节点直到到达叶子节点。

树具有的性质：

1. 树可以没有节点，这种情况下把树称为空树(empty tree)

2. 树的层次(layer)从根节点算起，即根节点算是第一层，根节点的子树根节点为第二层，以此类推

3. 把节点的子数棵树称为节点的度，而树中节点的最大的度称为树的度（也称为树的宽度）

4. 由于树中不存在环，且一条边连接两个节点，因此对有n个节点的树，边数一定是n-1。反之，满足连通、边数等于节点数减一的图一定是树。

5. 叶子节点被定义为度为0的节点，因此当树中只有一个节点（即只有根节点）时，根节点也算叶子节点。

6. 节点的深度(depth)是指从根节点（深度为1）开始自顶向下逐层累加至该节点时的深度值；节点的高度(height)是指从最底层的叶子节点(高度为1)开始自底向上逐层累加至该节点时的高度值。

   树的深度是指树中节点的最大深度，树的高度是指树中节点的最大高度。对于树而言，高度和深度是相等的。

7. 多棵树组合在一起称为森林(forest)，即森林是若干棵树的集合

##### 二叉树的递归定义

- 要么二叉树没有根节点，是一颗空树
- 要么二叉树由根节点、左子树、右子树组成，且左子树和右子树都是二叉树

这里需要注意一下度为2的树与二叉树之间的区别：度为2的树本质上是一种图，它并没有严格区分左子树和右子树；而二叉树虽然也是一种度为2的树，但是它的本质是一种数据结构，其左右子树是严格区分的，不能进行交换。

两种特殊的二叉树：

1. 满二叉树：每一层的节点个数都到达了当层能到达的最大节点数。
2. 完全二叉树：除了最下面的一层，每一层的节点个数都到达了当层能到达的最大节点数。满二叉树也属于完全二叉树。

一个节点的子树的根节点称为这个节点的孩子节点，而这个节点称为其孩子节点的父亲节点，同父亲节点的节点称为兄弟节点。

##### 二叉树的基本操作

二叉树使用链表来定义，但是和普通链表之间的区别在于，二叉树中的每个节点中存在两个指针，分别指向左右子树根节点，如果不存在左右子树，则将这个指针置为`nullptr`，所以二叉树节点的定义如下：

```c++
struct node{
    typename data;
    node * lchild;
    node * rchild;
};

node * newNode(int data){
    node * Node = new node;
    Node -> data = data;
    Node -> lchild = nullptr;
    Node -> rchild = nullptr;
    return Node;
}
```

而对于二叉树的操作有下面几种，二叉树的建立，二叉树节点查找、修改和删除。因为对于不同结构的树的删除操作不会有区别，所以这里将不会介绍删除相关的内容。

在介绍建立一个二叉树的操作之前，先看看在一个二叉树中插入一个元素的操作：

```c++
void insert(node * &root, int data){
    if(root == nullptr){
        root = newNode(data);
        return;
    }
    if(root -> lchild == nullptr)
        insert(root -> lchild, data);
    else if(root -> rchild == nullptr)
        insert(root -> rchild, data);
    else
        insert(root -> lchild, data);
}
```

上面的这个插入函数只是单纯的实现了节点的插入的功能，但是如果使用这样的函数来创建一个树的话，得到的树并不是一个完全二叉树，可以发现，每个节点的右子树都只有一个根节点，即每个节点的右子树都只有一层。

在上面个的代码中需要注意的是，函数中的参数`node * &root`，这是一个指针类型的引用变量，因为这里是要删除这个指针内保存的地址，比如从空指针指向一块动态申请的内存，而不是一般情况下，修改指针指向的内存中所存储的内容，所以需要将这个参数设置为引用变量。

在有了插入函数的情况下，就可以创建一个树了，实际上就是将数据依次插入一个初始值为空指针的node指针中：

```c++
#include <iostream>

struct node{
    int data;
    node * lchild;
    node * rchild;
};

node * newNode(int data){
    node * Node = new node;
    Node -> data = data;
    Node -> lchild = nullptr;
    Node -> rchild = nullptr;
    return Node;
}

void insert(node * &root, int data){
    if(root == nullptr){
        root = newNode(data);
        return;
    }
    if(root -> lchild == nullptr)
        insert(root -> lchild, data);
    else if(root -> rchild == nullptr)
        insert(root -> rchild, data);
    else
        insert(root -> lchild, data);
}

int main(){
    using namespace std;
    int array[5] = {1, 2, 3, 4, 5};
    node * root = nullptr;
    for(int i = 0; i < 5; i++)
        insert(root, array[i]);
    return 0;
}
```

在创建了一个树结构后，可以对树中的数据进行查找并修改：

```c++
#include <iostream>

struct node{
    int data;
    node * lchild;
    node * rchild;
};

node * newNode(int data){
    node * Node = new node;
    Node -> data = data;
    Node -> lchild = nullptr;
    Node -> rchild = nullptr;
    return Node;
}

void insert(node * &root, int data){
    if(root == nullptr){
        root = newNode(data);
        return;
    }
    if(root -> lchild == nullptr)
        insert(root -> lchild, data);
    else if(root -> rchild == nullptr)
        insert(root -> rchild, data);
    else
        insert(root -> lchild, data);
}

void search(node * root, int old, int x){
    if(root == nullptr)
        return;
    if(root -> data == old){
        root -> data = x;
        return;
    }
    search(root -> lchild, old, x);
    search(root -> rchild, old, x);
}

int main(){
    using namespace std;
    int array[5] = {1, 2, 3, 4, 5};
    node * root = nullptr;
    for(int i = 0; i < 5; i++)
        insert(root, array[i]);
    cout << root -> data << endl;
    search(root, 3, 0);
    node * l = root -> rchild;
    cout << l -> data;
    return 0;
}
```

##### 二叉树的遍历

二叉树的遍历方法有四种：先序遍历、中序遍历、后序遍历和层次遍历，其中前三种使用深度优先搜索(DFS)实现，而层次遍历使用广度优先搜索(BFS)实现。

> 深度优先搜索：以深度作为关键字进行搜索的过程，假如在一个迷宫内，那么深度优先搜索就是每到一个岔路口都随机选择一条路，然后一直走到死胡同后往回走。深度优先搜索能够使用递归的方法实现。
>
> 广度优先搜索：同样是迷宫的例子，没到一个岔路口，依次访问这个岔路口能到达的路口，然后再按这个顺序依次去访问这些岔路口能够到达下一个路口，以此类推。

###### 递归遍历

所以这里的前三种遍历方法，即先序遍历、中序遍历和后序遍历的思想都是一样的，就是通过递归的方式进行遍历，只不过这三种方法的遍历顺序不同：

- 先序遍历的遍历顺序是：根节点 $\to$ 左子树 $\to$ 右子树
- 中序遍历的遍历顺序是：左子树 $\to$ 根节点 $\to$ 右子树
- 后序遍历的遍历顺序是：左子树 $\to$ 右子树 $\to$ 根节点

例如下面这个例子，一个三层的满二叉树：

![](C:\Users\19021\Pictures\tree.png)

那么使用上面的哪三种遍历方法对这个树进行遍历输出的结果依次为：

先序遍历：`1 2 4 5 3 6 7 `

中序遍历：`4 2 5 1 6 3 7 `

后序遍历：`4 5 2 6 7 3 1 `

所以这三种遍历方法的实现如下：

先序遍历：

```C++
#include <iostream>

using namespace std;

struct node{
    int data;
    node * lchild;
    node * rchild;
};

node * newNode(int data){
    node * Node = new node;
    Node -> data = data;
    Node -> lchild = nullptr;
    Node -> rchild = nullptr;
    return Node;
}

void insert(node * &root, int x){
    if(root == nullptr){
        root = newNode(x);
        return;
    }
    if(root -> lchild == nullptr)
        insert(root -> lchild, x);
    else if(root -> rchild == nullptr)
        insert(root -> rchild, x);
    else
        insert(root -> lchild, x);
}

void preorder(const node * root){
    if(root == nullptr)
        return;
    cout << root -> data;
    preorder(root -> lchild);
    preorder(root -> rchild);
}

int main(){
    node * root = nullptr;
    for(int i = 0; i < 5; i++)
        insert(root, i + 1);
    insert(root -> rchild, 6);
    insert(root -> rchild, 7);
    preorder(root);
    return 0;
}
```

输出结果为：`1 2 4 5 3 6 7`

中序遍历：

```C++
#include <iostream>

using namespace std;

struct node{
    int data;
    node * lchild;
    node * rchild;
};

node * newNode(int data){
    node * Node = new node;
    Node -> data = data;
    Node -> lchild = nullptr;
    Node -> rchild = nullptr;
    return Node;
}

void insert(node * &root, int x){
    if(root == nullptr){
        root = newNode(x);
        return;
    }
    if(root -> lchild == nullptr)
        insert(root -> lchild, x);
    else if(root -> rchild == nullptr)
        insert(root -> rchild, x);
    else
        insert(root -> lchild, x);
}

void inorder(const node * root){
    if(root == nullptr)
        return;
    inorder(root -> lchild);
    cout << root -> data << " ";
    inorder(root -> rchild);
}

int main(){
    node * root = nullptr;
    for(int i = 0; i < 5; i++)
        insert(root, i + 1);
    insert(root -> rchild, 6);
    insert(root -> rchild, 7);
    inorder(root);
    return 0;
}
```

输出结果为：`4 2 5 1 6 3 7`

后序遍历：

```c++
#include <iostream>

using namespace std;

struct node{
    int data;
    node * lchild;
    node * rchild;
};

node * newNode(int data){
    node * Node = new node;
    Node -> data = data;
    Node -> lchild = nullptr;
    Node -> rchild = nullptr;
    return Node;
}

void insert(node * &root, int x){
    if(root == nullptr){
        root = newNode(x);
        return;
    }
    if(root -> lchild == nullptr)
        insert(root -> lchild, x);
    else if(root -> rchild == nullptr)
        insert(root -> rchild, x);
    else
        insert(root -> lchild, x);
}

void postorder(const node * root){
    if(root == nullptr)
        return;
    postorder(root -> lchild);
    postorder(root -> rchild);
    cout << root -> data << " ";
}

int main(){
    node * root = nullptr;
    for(int i = 0; i < 5; i++)
        insert(root, i + 1);
    insert(root -> rchild, 6);
    insert(root -> rchild, 7);
    postorder(root);
    return 0;
}
```

输出结果为：`4 5 2 6 7 3 1`

所以从输出结果来看，所谓先序中序和后序描述的其实是根节点的输出顺序，而左节点的输出一定是在右节点的前面，但不论是先序遍历还是后序遍历，都必须知道中序遍历序列才能唯一的确定一棵树。

> 下面看一个问题：给定一棵树的先序遍历序列和中序遍历序列，如何重建这个树
>
> 假设有一个树，
>
> 其先序遍历序列为：{$p_1, p_2, \dots, p_n$}
>
> 其中序遍历序列为：{$i_1, i_2, \dots, i_n$}
>
> 从遍历顺序可知，$p_1$是这棵树的根节点，而在中序遍历的序列中，根节点是左子树节点和右子树节点的分界线。
>
> 那么可以通过这样的方法恢复这个数的结构：
>
> 先遍历中序遍历序列，找到$i_k = p_1$
>
> 则{$i_1, i_2, \dots, i_{k-1}$}是左子树的中序遍历序列，且{$p_2,p_3,\dots,p_k$}是左子树的先序遍历序列
>
> {$i_{k+1},i_{k+2},\dots,i_n$}是右子树的中序遍历序列，且{$p_{k+1},p_{k+2},\dots,p_n$}是右子树的先序遍历序列
>
> 所以这样就可以通过递归算法实现上面的过程，从而恢复出这个树原来的结构。

###### 层序遍历

前面三种遍历方法都是通过递归实现的，或者说是基于深度优先搜索算法实现的，而层序遍历方法是通过非递归算法实现的，也就是说通过广度优先搜索算法实现的。

基于广度优先搜索的层序遍历的算法思想如下：

1. 创建一个队列
2. 将根节点加入队列
3. 取出队首的元素，并访问这个元素
4. 如果队首元素有左孩子，将这个左孩子加入队列
5. 如果队首元素有右孩子，将这个右孩子加入队列
6. 重复步骤3，直到队列为空

层序遍历的代码实现如下：

```c++
#include <iostream>
#include <queue>

struct node{
    int data;
    node * lchild;
    node * rchild;
};

node * newNode(int data){
    node * Node = new node;
    Node -> data = data;
    Node -> lchild = nullptr;
    Node -> rchild = nullptr;
    return Node;
}

void insert(node * &root, int x){
    if(root == nullptr){
        root = newNode(x);
        return;
    }
    if(root -> lchild == nullptr)
        insert(root -> lchild, x);
    else if(root -> rchild == nullptr)
        insert(root -> rchild, x);
    else
        insert(root -> lchild, x);
}

int main(){
    using namespace std;
    node * root = nullptr;
    for(int i = 0; i < 5; i++)
        insert(root, i + 1);
    insert(root -> rchild, 6);
    insert(root -> rchild, 7);
    queue<node *> q;
    q.push(root);
    while(!q.empty()){
        node * t = q.front();
        cout << t -> data << " ";
        if(t -> lchild != nullptr)
            q.push(t -> lchild);
        if(t -> rchild != nullptr)
            q.push(t -> rchild);
        q.pop();
    }
    return 0;
}
```

还是上面例子中的那棵树，输出结果为：`1 2 3 4 5 6 7`

借助层序遍历，可以计算出每个节点的高度：

```C++
#include <iostream>
#include <queue>

struct node{
    int data;
    int height;
    node * lchild;
    node * rchild;
};

node * newNode(int data){
    node * Node = new node;
    Node -> data = data;
    Node -> lchild = nullptr;
    Node -> rchild = nullptr;
    return Node;
}

void insert(node * &root, int x){
    if(root == nullptr){
        root = newNode(x);
        return;
    }
    if(root -> lchild == nullptr)
        insert(root -> lchild, x);
    else if(root -> rchild == nullptr)
        insert(root -> rchild, x);
    else
        insert(root -> lchild, x);
}

int main(){
    using namespace std;
    node * root = nullptr;
    for(int i = 0; i < 5; i++)
        insert(root, i + 1);
    insert(root -> rchild, 6);
    insert(root -> rchild, 7);
    queue<node *> q;
    q.push(root);
    root -> height = 1;
    while(!q.empty()){
        node * t = q.front();
        cout << t -> data << " ";
        if(t -> lchild != nullptr){
            q.push(t -> lchild);
            t -> lchild -> height = t -> height + 1;
        }
        if(t -> rchild != nullptr){
            q.push(t -> rchild);
            t -> rchild -> height = t -> height + 1;
        }
        q.pop();
    }
    return 0;
}
```

> 给定一个树的层序遍历序列和中序遍历序列，如何恢复这个树的结构？
>
> 比如现在有一个树，
>
> 中序遍历序列为：{$i_1,i_2,\dots,i_n$}
>
> 层序遍历序列为：{$l_1,l_2,\dots,l_n$}
>
> 首先，$l_1$是根节点，$l_2$是左子树的根节点，$l_3$是右子树的根节点。
>
> 那么可以根据中序遍历序列的特点，找到根节点将中序遍历序列进行划分，确定左右子树，从而恢复这个树的结构。

#### 树的遍历

这里所说的树是更为广义的树，而不是前面主要讲的二叉树。

因为是更为广义的树，所以不像二叉树那样能够确定每个树的子节点数都不超过2，因此这里需要采用树的静态实现：

```c++
struct node{
    int data;
    vector[int] child;
}Node[maxN];
```

上面的这段代码中，data为数据域，用于存储数据；而child为指针域，用于存储子节点的下标。Node为节点数组，用于存储所有的节点。

这里需要指出的是，如果不需要数据域，那么可以直接将树的静态实现写为：`vector<int> Node[maxN];`

##### 树的先根遍历

和二叉树的先序遍历一样，先访问根节点，然后依次访问左子树和右子树，方便使用递归算法实现：

```c++
void preorder(const int root){
    std::cout << Node[root].data << " ";
    for(int i = 0; i < Node[root].child.size(); i++)
        preorder(Node[root].child[i]);
}
```

上面这段代码需要注意的是，这里传递给递归函数的参数不再是指针而是当前节点的下标。

并且递归函数的递归边界隐式的设置为：`Node[root].child.size() == 0`

##### 树的层序遍历

层序遍历也和二叉树的层序遍历一样，创建一个队列，将当前节点的子节点都添加到队列中，然后输出队列：

```c++
void layerorder(const int root){
    queue<int> q;
    q.push(root);
    while(!q.empty()){
        int current = q.front();
        std::cout << Node[current].data << " ";
        for(int i = 0; i < Node[current].child.size(); i++)
            q.push(Node[current].child[i]);
        q.pop();
    }
}
```

#### 二叉查找树

二叉查找树(Binary Search Tree, BST)是一种特殊的二叉树，又成为排序二叉树、二叉搜索树、二叉排序树。

二叉查找树的递归定义如下：

- 要么二叉查找树是一个空树
- 要么二叉查找树由根节点、左子树和右子树组成，其中左子树和右子树都是二叉查找树，且左子树上所有节点的数据域均小于或等于根节点的数据域，右子树上所有节点的数据域均大于根节点的数据域。

所以二叉查找树的节点定义和二叉树的节点定义基本是一样的：

```c++
struct node{
	int data;  
  	node * lchild;
  	node * rchild;
};

node * newNode(int data){
    node * Node = new node;
    Node -> data = data;
    Node -> lchild = nullptr;
    Node -> rchild = nullptr;
    return Node;
}
```

##### 二叉查找树的基本操作

对二叉查找树的基本操作包括查找、插入、删除，这些操作其实都是在对于二叉树的基本操作的算法的基础上进行设计的。

###### 查找

由于二叉查找树的性质，如果待查找节点的数据域等于根节点的数据域，那么说明找到了相应节点；如果待查找节点的数据域小于根节点的数据域，那么说明待查找的节点在根节点的左子树中；如果待查找节点的数据域大于根节点的数据域，那么说明待查找的节点在根节点的右子树中。

因此，对二叉查找树中的节点的查找过程的代码实现如下：

```C++
void search(const node * root, int x){
    if(root == nullptr){
        std::cout << "search failed!" << std::endl;
        return;
    }
    if(root -> data == x){
        std::cout << root -> data << " founded" << std::endl;
        return;
    }else if(root -> data > x)
        search(root -> lchild, x);
    else
        search(root -> rchild, x);
}
```

###### 插入

二叉查找树的插入过程和查找过程有比较大的相似性，区别在于：如果查找失败，就创建一个新节点；如果查找成功就说明树中已经存在这样的节点，则停止插入；

所以代码实现如下：

```C++
void insert(node * &root, int x){
	if(root == nullptr){
        root = newNode(x);
        return;
    }
    if(root -> data == x){
        std::cout << root -> data << " already exist.";
        return;
    }else if(root -> data > x)
        insert(root -> lchild, x);
    else
        insert(root -> rchild, x);
}
```

在有了二叉查找树的插入操作后，建立一个二叉查找树的过程就是将序列中的数据依次插入一个树中的过程。

```C++
int main(){
	node * root;
    int data[] = {5, 3, 7, 4, 2, 8, 6};
    for(int i = 0; i < 7; i++)
        insert(root, data[i]);
    return 0;
}
```

需要注意的是，因为二叉查找树的性质，即使使用一组数据，如果它们的顺序不同，最终得到的二叉查找树的结构也会不同。

###### 删除

二叉查找树的节点删除过程比较复杂，因为需要保证在删除了一个节点后得到的二叉树依然是一个二叉查找树。

为了保证在删除一个节点后得到的二叉树依然是一个二叉查找树，通常采用的操作是，找到比当前节点小的最大节点，将这个节点称为当前节点的前驱，或者找到比当前节点大的最小节点，将这个节点称为当前节点的后继。然后用这个节点的前驱或者后继的数据域覆盖当前节点的数据域，最后再删除这个节点原来的前驱节点或者后继节点。

因为二叉查找树的性质，要找到一个节点的前驱节点或者后继节点都是比较容易的，要找前驱节点，那么就在当前节点的左子树中不断查找右孩子节点，直到某个节点不存在右孩子节点，那么这个节点就是当前节点的前驱；要找后继节点，那么就在当前节点的右子树中不断查找左孩子节点，直到某个节点不存在左孩子节点，那么这个节点就是当前节点的后继。

在删除一个节点前，需要先找到这个节点，然后查找这个节点的前驱或者后继来代替这个节点的数据域。

具体思想是：如果这个节点是也直接点，那么就直接删除；否则，如果这个节点的左子树不为空，那么就找到这个节点的前驱节点来替换这个节点的数据域；否则，如果这个这个节点的右子树不为空，那么就找到这个节点的后继节点来替换这个节点的数据域。

其代码实现如下：

```c++
#include <iostream>

struct node{
    int data;
    node * lchild;
    node * rchild;
};

node * newNode(int data){
    node * Node = new node;
    Node -> data = data;
    Node -> lchild = nullptr;
    Node -> rchild = nullptr;
    return Node;
}

void Search(const node * root, int x){
    if(root == nullptr)
        return;
    if(root -> data == x){
        std::cout << root -> data << " founded.\n";
        return;
    }else if(root -> data > x)
        Search(root -> lchild, x);
    else
        Search(root -> rchild, x);
}

void Insert(node * &root, int x){
    if(root == nullptr){
        root = newNode(x);
        return;
    }
    if(root -> data == x){
        std::cout << root -> data << "already exist.\n";
        return;
    }else if(root -> data > x)
        Insert(root -> lchild, x);
    else
        Insert(root -> rchild, x);
}

void Delete(node * &root, int x){
    if(root == nullptr)
        return;
    if(root -> data == x){
        if(root -> lchild == nullptr && root -> rchild == nullptr){
            delete root;
            root = nullptr;
        }else if(root -> lchild != nullptr){
            node * pre = root -> lchild;
            while(pre -> rchild != nullptr)
                pre = pre -> rchild;
            root -> data = pre -> data;
            Delete(root -> lchild, pre -> data);
        }else{
            node * next = root -> rchild;
            while(next -> lchild != nullptr)
                next = next -> lchild;
            root -> data = next -> data;
            Delete(root -> rchild, next -> data);
        }
    }else if(root -> data > x)
        Delete(root -> lchild, x);
    else
        Delete(root -> rchild, x);
}

void preorder(const node * root){
    if(root == nullptr)
        return;
    std::cout << root -> data << " ";
    preorder(root -> lchild);
    preorder(root -> rchild);
}

int main(){
    node * root = nullptr;
    int data[] = {5, 3, 7, 4, 2, 8, 6};
    for(int i = 0; i < 7; i++)
        Insert(root, data[i]);
    preorder(root);
    Delete(root, 5);
    std::cout << std::endl;
    preorder(root);
    return 0;
}
```

上面这段代码的输出为：

`5 3 2 4 7 6 8`

`4 3 2 7 6 8`

这里需要注意的是，对一个指针使用delete运算符后，只是释放了这个指针所指向的内存，但是这个指针并不等于`nullptr`:

```C++
#include <iostream>
#include <string>

int main(){
    using namespace std;
    int * p =new int(5);
    delete p;
    cout << bool(p == nullptr) << endl;	//0
    return 0;
}
```

所以这里在释放了内存后，还需要将指针的值置为`nullptr`。

##### 二叉查找树的性质

二叉查找树的性质，左子树节点数据域 < 根节点数据域 < 右子树节点数据域

而中序遍历的顺序也是：左子树 $\to$ 根节点 $\to$ 右子树

所以如果对一个二叉查找树使用中序遍历的话，得到的中序遍历序列也一定是一个升序序列：

```c++
#include <iostream>

struct node{
    int data;
    node * lchild;
    node * rchild;
};

node * newNode(int data){
    node * Node = new node;
    Node -> data = data;
    Node -> lchild = nullptr;
    Node -> rchild = nullptr;
    return Node;
}

void Search(const node * root, int x){
    if(root == nullptr)
        return;
    if(root -> data == x){
        std::cout << root -> data << " founded.\n";
        return;
    }else if(root -> data > x)
        Search(root -> lchild, x);
    else
        Search(root -> rchild, x);
}

void Insert(node * &root, int x){
    if(root == nullptr){
        root = newNode(x);
        return;
    }
    if(root -> data == x){
        std::cout << root -> data << "already exist.\n";
        return;
    }else if(root -> data > x)
        Insert(root -> lchild, x);
    else
        Insert(root -> rchild, x);
}

void Delete(node * &root, int x){
    if(root == nullptr)
        return;
    if(root -> data == x){
        if(root -> lchild == nullptr && root -> rchild == nullptr){
            delete root;
            root = nullptr;
        }else if(root -> lchild != nullptr){
            node * pre = root -> lchild;
            while(pre -> rchild != nullptr)
                pre = pre -> rchild;
            root -> data = pre -> data;
            Delete(root -> lchild, pre -> data);
        }else{
            node * next = root -> rchild;
            while(next -> lchild != nullptr)
                next = next -> lchild;
            root -> data = next -> data;
            Delete(root -> rchild, next -> data);
        }
    }else if(root -> data > x)
        Delete(root -> lchild, x);
    else
        Delete(root -> rchild, x);
}

void inorder(const node * root){
    if(root == nullptr)
        return;
    inorder(root -> lchild);
    std::cout << root -> data << " ";
    inorder(root -> rchild);
}
```

上面这段代码输出为：

`2 3 4 5 6 7 8`

`2 3 4 6 7 8`

#### 平衡二叉树

二叉查找树是在二叉树的基础上加上“左子树节点数据域 < 根节点数据域 < 右子树节点数据域”的性质得到的。

一般情况下，由于二叉查找树的性质，查找某个节点的时间复杂度不会超过`O(logN)`

现在考虑一种情况，比如用于构建二叉查找树的数据序列为{1, 2, 3, 4, 5}，那么得到的二叉查找树中的每个节点都只有右孩子节点，在这种情况下，在二叉查找树中查找某个节点的时间复杂度为`O(N)`

所以为了使二叉查找树查找元素的时间复杂度保持在`O(logN)`的水平，需要对这个树的结构进行调整。在二叉查找树的基础上加上平衡的要求，就是所谓的平衡二叉树，也称为AVL树，它是由两个苏联数学家Adelse-Velskil和Landis提出的，AVL树依然是一个二叉查找树。

这里使用数学的方法来定义“平衡”这个概念，即对于任意一个节点，其左子树的高度和右子树的高度的差值的绝对值不超过1。一般将左子树和右子树的高度差值的称为这个节点的平衡因子。

如果能保证每个节点的平衡因子的绝对值不超过1，那么就能保证二叉查找树的高度不超过`O(logN)`，那么查找某个节点的时间复杂度也不会超过`O(logN)`。

所以要保证一个树是平衡的，需要计算出每个节点的平衡因子，这需要改变节点的数据结构：

```c++
struct node{
    int data;
    int height;
    node * lchild;
    node * rchild;
};

node * newNode(int x){
    node * Node = new node;
    node -> lchild = nullptr;
    node -> rchild = nullptr;
    node -> height = 1;
    return Node;
}
```

当插入节点时，需要对节点的高度进行更新：

```C++
int getHeight(node * root){
    if(root == nullptr) return 0;
    else return root -> height;
}

void updateHeight(node * root){
    root -> height = max(getHeight(root -> lchild), getHeight(root -> rchild)) + 1;
}
```

有了高度，就可以计算每个节点的平衡因子：

```C++
int getBalanceFactor(node * root){
    return getHeight(root -> lchild) - getHeight(root -> rchild);
}
```

##### 平衡二叉树的基本操作

平衡二叉树与另外两种树的在操作上的差异在于插入操作上。

在介绍插入操作之前，需要先了解平衡二叉树的左旋右旋操作，这两种操作用于调整平衡二叉树的结构。

左旋：

如果要对一个节点root进行左旋操作，那么应该执行下面的操作：

1. 将root的右孩子节点设为root右孩子节点的左孩子节点
2. 将root原来的右孩子节点的左孩子节点设为root节点
3. 返回root原来的右孩子节点

图示如下

![](C:\Users\19021\Pictures\LeftRotate.png)

代码实现如下：

```C++
void leftRotate(node * &root){
	node * temp = root -> rchild;
    root -> rchild = temp -> lchild;
    temp -> lchild = root;
    root = temp;
}
```

右旋：

如果要对一个节点进行右旋操作，那么应该执行下面的操作：

1. 将root的左孩子节点设为root左孩子节点的右孩子节点
2. 将root原来的左孩子节点的右孩子节点设为root节点
3. 返回root原来的左孩子节点

图示如下

![](C:\Users\19021\Pictures\rightRotate.png)

代码实现如下：

```c++
void rightRotate(node * &root){
    node * temp = root -> lchild;
    root -> lchild = root -> lchild -> rchild;
    temp -> rchild = root;
    root = temp;
}
```

可以发现平衡二叉树的左旋与右旋操作都是刚好对称的。

有了平衡二叉树的左旋与右旋操作后，可以借助这两个操作来调整树的结构。而调整结构的思想也比较简单，只要把最靠近插入节点失衡节点调整到正常，路径上的所有节点就都会平衡。

一旦发现某个节点的平衡因子的绝对值为2，那么就说明出现了失衡节点，根据失衡节点以及其孩子节点的平衡因子的取值情况，可以将失衡的树形结构分为下面四种情况：

- LL形：失衡节点平衡因子为2，且失衡节点的左孩子节点的平衡因子为1
- LR形：失衡节点平衡因子为2，且失衡节点的左孩子节点的平衡因子为-1
- RL形：失衡节点平衡因子为-2，且失衡节点的右孩子节点的平衡因子为1
- RR形：失衡节点平衡因子为-2，且失衡节点的右孩子节点的平衡因子为-1

如下图：

![](C:\Users\19021\Pictures\AVLcase.png)

从上面的图可以发现：

- 如果发现失衡节点时的树形为LL形的，那么对失衡节点进行一次右旋即可平衡
- 如果发现失衡节点时的树形为LR形的，那么对这个失衡节点的左孩子节点进行一次左旋即可使树形变成LL形
- 如果发现失衡节点时的树形为RR形的，那么对失衡节点进行一次左旋即可平衡
- 如果发现失衡节点时的树形为RL形的，那么对这个失衡节点的右孩子节点进行一次右旋即可使树形变成RR形

根据上面的这四条原则，可以在插入节点时进行判断并进行调整，代码实现如下：

```C++
#include <iostream>
#include <algorithm>

struct node{
    int data;
    int height;
    node * lchild;
    node * rchild;
};

node * newNode(int x){
    node * Node = new node;
    Node -> data = x;
    Node -> height = 1;
    Node -> lchild = nullptr;
    Node -> rchild = nullptr;
    return Node;
}

int getHeight(const node * root){
    if(root == nullptr) return 0;
    else return root -> height;
}

void updateHeight(node * root){
    root -> height = std::max(getHeight(root -> lchild), getHeight(root -> rchild)) + 1;
}

int getBalanceFactor(const node * root){
    return getHeight(root -> lchild) - getHeight(root -> rchild);
}

void leftRotate(node * &root){
    node * temp = root -> rchild;
    root -> rchild = root -> rchild -> lchild;
    temp -> lchild = root;
    root = temp;
}

void rightRotate(node * &root){
    node * temp = root -> lchild;
    root -> lchild = root -> lchild -> rchild;
    temp -> rchild = root;
    root = temp;
}

void Insert(node * &root, int x){
    if(root == nullptr){
        root = newNode(x);
        return;
    }
    if(root -> data == x){
        std::cout << root -> data << " already exist.\n";
        return;
    }else if(root -> data > x){
        Insert(root -> lchild, x);
        updateHeight(root);
        if(getBalanceFactor(root) == 2){
            if(getBalanceFactor(root -> lchild) == 1)
                rightRotate(root);
            else{
                leftRotate(root -> lchild);
                rightRotate(root);
            }
            updateHeight(root);
        }
    }else{
        Insert(root -> rchild, x);
        updateHeight(root);
        if(getBalanceFactor(root) == -2){
            if(getBalanceFactor(root -> rchild) == -1)
                leftRotate(root);
            else{
                rightRotate(root -> rchild);
                leftRotate(root);
            }
            updateHeight(root);
        }
    }
}

void preorder(const node * root){
    if(root == nullptr)
        return;
    std::cout << root -> data << " ";
    preorder(root -> lchild);
    preorder(root -> rchild);
}

int main(){
    node * root = nullptr;
    int data[] = {1, 2, 3, 4, 5, 6, 7};
    for(int i = 0; i < 7; i++)
        Insert(root, data[i]);
    preorder(root);
    return 0;
}
```

上面这段代码创建了一个树，并且在这个树种依次插入{1, 2, 3, 4, 5, 6, 7}，按照平衡二叉树的方式插入，最后再按照先序遍历的方式遍历这个平衡二叉树，最后的遍历结果为：`4 2 1 3 6 5 7`

而平衡二叉树本质也是一个二叉查找树，所以中序遍历序列为：`1 2 3 4 5 6 7`

所以可以根据前序序列和中序序列恢复这个数的结构，可以发现这个树确实具有平衡结构。

#### 并查集

并查集是一种维护集合的数据结构，其名字中的“并”、“查”就是合并(Union)和查找(Find)，也就是说并查集支持下面两种操作：

- 合并：合并两个集合
- 查找：判断两个元素是否在同一个集合

这种数据结构的实现其实就是一个数组：`int father[N];`

其中`father[i]`表示元素`i`的父亲节点，而父亲节点本身也是集合内的元素。

对于一个集合来说，只能有一个根节点，作为这个集合的标识。而判别一个节点是否是根节点的方式，就是看这个根节点的父亲节点是否就是其本身，即`father[i] == i ?`

##### 并查集的基本操作

初始化

一开始，每个节点都是单独的集合，即每个节点都是根节点：

`for(int i = 0; i < N; i++) father[i] = i;`

查找

查找过程就是给定一个元素，返回其所在集合的根节点

```c++
int Find(int x){
    while(father[x] != x)
        x = father[x];
    return x;
}
```

合并

合并是指把两个集合合并成一个集合，给定两个元素，需要先判断这两个元素是否属于同一个集合，如果属于同一个集合，那么就不需要再进行合并，只有在两个元素不属于同一个集合的情况下才进行合并。而合并过程一般是将一个元素所属集合的根节点的父亲节点设置为另一个集合根节点。

所以代码实现如下：

```c++
void Union(int a, int b){
    int ra = Find(a);
    int rb = Find(b);
    if(ra == rb)
        return;
    else
        father[ra] = rb;
}
```

##### 并查集的性质

在合并过程中，只对两个不同的集合进行合并处理，如果两个元素在同一个集合中，那么就不会对其执行合并操作，这就保证了在同一个集合中一定不会产生环，即并查集的每一个集合都是一个树。‘

##### 路径压缩

现在考虑一种情况，一个并查集的结构是一条链状结构，

比如：`father[0] = 0; father[1] = 0; father[2] = 1;...`

所以如果在找到某个元素n的根节点，那么其时间复杂度为`O(n)`，当n十分大的时候，这个时间复杂度是不可接受的。

但如果只是为了找到根节点，那么完全可以将一条路径上的所有节点的父亲节点都设置为根节点，那么要找到一个节点的根节点的时间复杂度就是`O(1)`，代码实现如下：

```c++
int findFather(int v){
    int root = v;
    while(father[root] != root)
        root = father[root];
    while(current != root){
        int temp = v;
        v = father[v];
        father[temp] = root;
    }
    return root;
}
```

上面的这段代码将元素`v`到其根节点路径上的所有节点的父亲节点都设置成了根节点。

#### 堆

<span id = "heap"></span>

##### 堆的定义

堆是一个完全二叉树，树中每个节点的值都不小于（或不大于）其左右孩子的值。这里需要注意堆与二叉查找树之间的区别，堆的升序关系是体现在层次上的，而二叉查找树的升序关系是体现在其中序遍历序列上的。

如果父亲节点的值大于或等于孩子节点的值，那么称这样的堆为大顶堆，这时每个节点的值都是以这个节点为根节点的子树的最大值；

如果父亲节点的值小于或等于孩子节点的值，那么称这样的堆为小顶堆，这时每个节点的值都是以这个节点为根节点的子树的最小值。

这里以大顶堆为例，给定一个序列，现对其按照层序创建一个二叉树，即初始堆，然后对初始堆进行调整，使其每个子树中最大的点都是根节点。

按照层序创建一个二叉树的方法类似于层序遍历，可以借助队列来实现：

```C++
#include <iostream>
#include <queue>

using namespace std;

struct node{
    int data;
    node * lchild;
    node * rchild;
};

node * newNode(int data){
    node * Node = new node;
    Node -> data = data;
    Node -> lchild = nullptr;
    Node -> rchild = nullptr;
    return Node;
}

node * &Find(node * &root, int x){
    if(root == nullptr)
        return root;
    if(root -> data == x)
        return root;
    else{
        node * &lf = Find(root -> lchild, x);
        node * &rf = Find(root -> rchild, x);
        if(lf != nullptr && lf -> data == x)
            return lf;
        else if(rf != nullptr && rf -> data == x)
            return rf;
        else
            return root;
    }
}

void Create(node * &root, queue<int> &data){
    queue<int> child = data;
    while(!child.empty()){
        int i = data.front();
        data.pop();
        if(root == nullptr){
            root = newNode(i);
            child.pop();
        }
        node * &rt = Find(root, i);
        int l = child.front();
        child.pop();
        int r = child.front();
        child.pop();
        if(l !=0 )
            rt -> lchild = newNode(l);
        if(r != 0)
            rt -> rchild = newNode(r);
    }
}

void inorder(const node * root){
    if(root == nullptr)
        return;
    inorder(root -> lchild);
    cout << root -> data << " ";
    inorder(root -> rchild);
}

void preorder(const node * root){
    if(root == nullptr)
        return;
    cout << root -> data << " ";
    preorder(root -> lchild);
    preorder(root -> rchild);
}

int main(){
    queue<int> q;
    node * root = nullptr;
    for(int i = 0; i < 7; i++)
        q.push(i + 1);
    Create(root, q);
    cout << "inorder traverse: ";
    inorder(root);
    cout << endl;
    cout << "preorder traverse: ";
    preorder(root);
    return 0;
}
```

上面这段代码中，以{1, 2, 3, 4, 5, 6, 7}的顺序按照层序创建了一个二叉树，然后再对这个二叉树先后进行中序遍历和前序遍历，输出结果如下：

`inorder traverse: 4 2 5 1 6 3 7`

`preorder traverse: 1 2 4 5 3 6 7`

可以将这个数的结构回复出来，可以发现这个树确实是按层序创建的。

> 这里需要注意一下`node * &Find(node * &root, int x);`函数，这个函数在以`root`为根节点的树中寻找数据域为x的节点，并且返回这个节点的引用：
>
> ```c++
> node * &Find(node * &root, int x){
>     if(root == nullptr)
>         return root;
>     if(root -> data == x)
>         return root;
>     else{
>         node * &lf = Find(root -> lchild, x);
>         node * &rf = Find(root -> rchild, x);
>         if(lf != nullptr && lf -> data == x)
>             return lf;
>         else if(rf != nullptr && rf -> data == x)
>             return rf;
>         else
>             return root;
>     }
> }
> ```
>
> 这个函数其实也可以用于前面的二叉树章节中一些函数的实现。

调整堆的过程比较简单，从下往上遍历，如果一个节点的孩子节点的数据域小于这个节点，就调换这两个节点的数据域。

代码实现如下：

```C++
#include <iostream>
#include <queue>

using namespace std;

struct node{
    int data;
    node * lchild;
    node * rchild;
};

node * newNode(int data){
    node * Node = new node;
    Node -> data = data;
    Node -> lchild = nullptr;
    Node -> rchild = nullptr;
    return Node;
}

node * &Find(node * &root, int x){
    if(root == nullptr)
        return root;
    if(root -> data == x)
        return root;
    else{
        node * &lf = Find(root -> lchild, x);
        node * &rf = Find(root -> rchild, x);
        if(lf != nullptr && lf -> data == x)
            return lf;
        else if(rf != nullptr && rf -> data == x)
            return rf;
        else
            return root;
    }
}

void Create(node * &root, queue<int> &data){
    queue<int> child = data;
    while(!data.empty()){
        int i = data.front();
        data.pop();
        if(root == nullptr){
            root = newNode(i);
            child.pop();
        }
        node * &rt = Find(root, i);
        int l = child.front();
        child.pop();
        int r = child.front();
        child.pop();
        if(l != 0)
            rt -> lchild = newNode(l);
        if(r != 0)
            rt -> rchild = newNode(r);
    }
}

void Adjust(node * &root){
    if(root == nullptr)
        return;
    Adjust(root -> lchild);
    Adjust(root -> rchild);
    if(root -> lchild != nullptr && (root -> data) < (root -> lchild -> data)){
        int temp = root -> data;
        root -> data = root -> lchild -> data;
        root -> lchild -> data = temp;
        Adjust(root -> lchild);
    }
    if(root -> rchild != nullptr && (root -> data) < (root -> rchild -> data)){
        int temp = root -> data;
        root -> data = root -> rchild -> data;
        root -> rchild -> data = temp;
        Adjust(root -> rchild);
    }
}

void inorder(const node * root){
    if(root == nullptr)
        return;
    inorder(root -> lchild);
    cout << root -> data << " ";
    inorder(root -> rchild);
}

void preorder(const node * root){
    if(root == nullptr)
        return;
    cout << root -> data << " ";
    preorder(root -> lchild);
    preorder(root -> rchild);
}

int main(){
    queue<int> q;
    node * root = nullptr;
    //int data[] = {85, 55, 82, 57, 68, 92, 99, 98, 66, 56};
    //for(int i = 0; i < 10; i++)
    //    q.push(data[i]);
    for(int i = 0; i < 7; i++)
        q.push(i + 1);
    Create(root, q);
    cout << "inorder traverse: ";
    inorder(root);
    cout << endl;
    cout << "preorder traverse: ";
    preorder(root);
    cout << endl;
    Adjust(root);
    cout << "After adjust:\n";
    cout << "inorder traverse: ";
    inorder(root);
    cout << endl;
    cout << "preorder traverse: ";
    preorder(root);
    cout << endl;
    return 0;
}
```

上面这段代码先是按照层序的方式以序列{1, 2, 3, 4, 5, 6, 7}创建了一个二叉树，然后对其从下往上调整，使其称为一个堆，代码的输出内容如下：

`inorder traverse: 4 2 5 1 6 3 7`

`preorder traverse: 1 2 4 5 3 6 7`

`After adjust:`

`inorder traverse: 1 4 2 7 3 6 5`

`preorder traverse: 7 4 1 2 6 3 5`

通过先后两次的中序遍历和先序遍历序列，可以将树的结构恢复出来：

![](C:\Users\19021\Pictures\heap.png)

> 在上面的这段代码中需要注意的是，因为在调整节点位置的时候整个树已经建立好了，所以这里的递归是先递归到叶子节点，然后再执行交换操作。

由于这里在创建一个树的时候借助队列来实现层序插入节点，也就是说在创建一个初始堆的时候就必须是完整的数据，所以这里不支持节点的增删操作。

为了更直观的表现堆的一些特征和处理思想，上面在介绍堆相关的内容时使用动态内存的方式来对其进行实现，但实际上一般是使用数组的方式来表示一个堆。

用数组的方式的来实现堆，不仅更加简介，而且可以更方便的计算不同操作的时间复杂度，并且在后面介绍堆排序时能更方便进行处理。

##### 堆的静态实现

使用数组实现一个完全二叉树的方法如下：

如果将第一个节点编号为`1`号，而将`1`号节点的左孩子编号为`2`号，`1`号节点的右孩子编号为`3`号；不难发现，第`i`号节点的左孩子编号为`2i`号，第`i`号节点的右孩子编号为`2i+1`号。

这样，就可以将一个完全树的所有节点存储在一个数组中。

> 其实上面通过按照层序创建树的思想也与这里的思想类似。

所以一个初始堆的创建过程：`int heap[maxN];`

然后就是对初始堆进行调整：

```C++
void downAdjust(const int low, const int high){
    int i = low, j = 2 * i;
    while(j <= high){
        if(j + 1 <= high && heap[j + 1] > heap[j])
            j = j + 1;
        if(heap[j] > heap[i]){
            int temp = heap[i];
            heap[i] = heap[j];
            heap[j] = temp;
            i = j;
            j = 2 * i;
        }else
            break;
    }
}
```

上面的这个函数用于调整heap[low]\~heap[high]范围内的节点的顺序。

>这里可以将代码和前面用于调整结构的代码进行比较：
>
>```c++
>void Adjust(node * &root){
>    if(root == nullptr)
>        return;
>    Adjust(root -> lchild);
>    Adjust(root -> rchild);
>    if(root -> lchild != nullptr && (root -> data) < (root -> lchild -> data)){
>        int temp = root -> data;
>        root -> data = root -> lchild -> data;
>        root -> lchild -> data = temp;
>        Adjust(root -> lchild);
>    }
>    if(root -> rchild != nullptr && (root -> data) < (root -> rchild -> data)){
>        int temp = root -> data;
>        root -> data = root -> rchild -> data;
>        root -> rchild -> data = temp;
>        Adjust(root -> rchild);
>    }
>}
>```
>
>这段代码是使用动态链表实现堆，然后使用递归算法实现堆的调整过程。
>
>然而堆的静态实现版本中，并没有使用递归实现。
>
>但是两个版本的算法思想几乎是相同的，递归版本是先遍历到最底层的具有孩子节点的节点，然后将其数据域与两个孩子节点的数据域进行比较交换，交换完成后，再对刚刚交换了的孩子节点进行一次调整。
>
>静态版本的`downAdjust()`也是一样的思想，先用一个临时变量`i`记录当前节点的编号，然后在看其是否孩子节点，最后在进行比较交换，交换完成后，再对刚刚交换过的孩子节点进行一次调整。

需要注意的是，因为在上一节里面堆的实现是采用动态链表实现的，在进行调整的时候已经创建了一个完整的初始堆，所以调整过程也是从叶子节点往上调整的。

但是是采用静态实现的方法，所以可以确定只有heap[1]\~heap[n/2]之间的节点采用孩子节点，也就是说只有这些节点才需要进行调整。这里的`downAdjust()`的含义是向下调整，意思是将父亲节点于孩子节点进行比较然后进行交换。

所以调整一个初始堆的过程就是从第`i = n/2`号节点开始依次往`1`号节点进行调整。

代码实现如下：

```c++
#include <iostream>

const int maxN = 100;

int heap[maxN];

int n;

void downAdjust(const int low, const int high){
    int i = low, j = 2 * i;
    while(j <= high){
        if(j + 1 <= high && heap[j + 1] > heap[j])
            j = j + 1;
        if(heap[j] > heap[i]){
            int temp = heap[i];
            heap[i] = heap[j];
            heap[j] = temp;
            i = j;
            j = 2 * i;
        }else
            break;
    }
}

int main(){
    using namespace std;
    int data[] = {85, 55, 82, 57, 68, 92, 99, 98, 66, 56};
    //initialization
    for(int i = 0; i < 10; i++)
        heap[i + 1] = data[i];
    n = 10;
    for(int i = n / 2; i >= 1; i--)
        downAdjust(i, n);
    for(int i = 1; i <= n; i++)
        cout << heap[i] << " ";
    return 0;
}
```

输出为：`99 98 92 66 68 85 82 57 55 56`

> 这其实就是一个完全二叉树的层序递归序列，前面提到过不论是先序遍历、后序遍历还是层序遍历序列，都必须在知道中序遍历序列的情况下才能恢复出一个二叉树的结构。
>
> 但是这里有所不同，因为是使用数组来简洁地实现一个树，所以是相当于是按层序依次将数据“填入”一个完全二叉树的，所以知道层序遍历序列就可以知道这个完全二叉树的结果，只需要再次按照层序依次将数据“填入”一个完全二叉树即可。

堆的调整过程的时间复杂度为`O(n)`

在堆的静态实现中，可以比较方便的实现堆中节点的增加和删除操作：

```c++
void Delete(int x){
    heap[x] = heap[n--];
    downAdjust(x, n);
}
```

而添加一个节点的过程相对比较复杂，添加一个节点后同样也要进行调整，但是和上面的向下调整不同的是，这里采用向上调整，即孩子节点与父亲节点进行比较交换。

向上调整：

```c++
void upAdjust(int low, int high){
    int i = high, j = i / 2;
    while(j >= low){
        if(heap[i] > heap[j]){
            int temp = heap[i];
            heap[i] = heap[j];
            heap[j] = temp;
            i = j;
            j = i / 2;
        }else
            break;
    }
}
```

所以添加元素的过程就是先将元素添加到最后，再进行一次`1~n`范围的向上调整即可：

```C++
#include <iostream>

const int maxN = 100;

int heap[maxN];

int n;

void downAdjust(const int low, const int high){
    int i = low, j = 2 * i;
    while(j <= high){
        if(j + 1 <= high && heap[j + 1] > heap[j])
            j = j + 1;
        if(heap[j] > heap[i]){
            int temp = heap[i];
            heap[i] = heap[j];
            heap[j] = temp;
            i = j;
            j = 2 * i;
        }else
            break;
    }
}

void Delete(int x){
    heap[x] = heap[n--];
    downAdjust(x, n);
}

void upAdjust(int low, int high){
    int i = high, j = i / 2;
    while(j >= low){
        if(heap[i] > heap[j]){
            int temp = heap[i];
            heap[i] = heap[j];
            heap[j] = temp;
            i = j;
            j = i / 2;
        }else
            break;
    }
}

void Insert(int data){
    heap[++n] = data;
    upAdjust(1, n);
}

int main(){
    using namespace std;
    int data[] = {85, 55, 82, 57, 68, 92, 99, 98, 66, 56};
    //initialization
    for(int i = 0; i < 10; i++)
        heap[i + 1] = data[i];
    n = 10;
    //Adjust
    for(int i = n / 2; i >= 1; i--)
        downAdjust(i, n);
    for(int i = 1; i <= n; i++)
        cout << heap[i] << " ";
    cout << endl;
    Delete(1);
    for(int i = 1; i <= n; i++)
        cout << heap[i] << " ";
    cout << endl;
    Insert(97);
    for(int i = 1; i <= n; i++)
        cout << heap[i] << " ";
    return 0;
}
```

代码输出：

`99 98 92 66 68 85 82 57 55 56`

`98 68 92 66 56 85 82 57 55`

`98 97 92 66 68 85 82 57 55 56`

##### 堆排序

不难发现，大顶堆中的第一个节点是整个堆中最大的数，根据这一性质，可以实现堆排序。

建好一个堆后，取出第一个数，那么这个数就是最大的数，将其放在数组的最后；然后再进行一次`1~n-1`范围内的向下调整，得到的堆的第一个元素是`1~n-1`范围内的最大元素；重复上面的操作，直到向下调整的范围中只有一个元素。

代码实现如下：

```c++
#include <iostream>

const int maxN = 100;

int heap[maxN];

int n;

void downAdjust(const int low, const int high){
    int i = low, j = 2 * i;
    while(j <= high){
        if(j + 1 <= high && heap[j + 1] > heap[j])
            j = j + 1;
        if(heap[j] > heap[i]){
            int temp = heap[i];
            heap[i] = heap[j];
            heap[j] = temp;
            i = j;
            j = 2 * i;
        }else
            break;
    }
}

void heap_sort(){
    for(int i = n; i > 1; i--){
        int temp = heap[i];
        heap[i] = heap[1];
        heap[1] = temp;
        downAdjust(1, i-1);
    }
}

int main(){
    using namespace std;
    int data[] = {85, 55, 82, 57, 68, 92, 99, 98, 66, 56};
    //initialization
    for(int i = 0; i < 10; i++)
        heap[i + 1] = data[i];
    n = 10;
    //Adjust
    for(int i = n / 2; i >= 1; i--)
        downAdjust(i, n);
    //sort
    heap_sort();
    for(int i = 1; i <= n; i++)
        cout << heap[i] << " ";
    return 0;
}
```

代码输出：

`55 56 57 66 68 82 85 92 98 99`

现在看看这个堆排序算法的时间复杂度：创建一个堆的时间复杂度为`O(n)`。

在创建了一个堆的情况下进行堆排序过程，因为每次`downAdjust()`的时间复杂度不超过`O(logn)`，每个元素都进行了一次`downAdjust()`，所以这个过程的时间复杂度为`O(nlogn)`。

所以整个排序过程的时间复杂度为`O(nlogn)`。

#### priority_queue类

priority_queue又称为优先队列，其队首元素始终是当且队列中优先级最高的元素，其底层实现是借助堆来实现的。

可以在任何时候往优先队列里添加元素，而优先队列的底层堆结构能够随时进行调整，使其队首的元素始终是优先级最大的。

要使用priority_queue类，需要在头文件中添加queue头文件，即`#include<queue>`，并且声明名称空间为std。

##### 声明priority_queue对象

和其他的STL容器类一样，声明priority_queue对象的通用格式为：

`priority_queue<typename> name;`

其中的`typename`可以任何合法类型参数。

##### 访问priority_queue容器内的元素

和一般的队列不同的是，priority_queue队列并没有`front()`和`back()`函数，而只有一个`top()`方法用于访问队首元素，也就是优先级最高的元素。

##### 常用的方法

push()方法，用于将一个元素添加到队列中，通过对堆的了解，可以直到这个方法的时间复杂度为`O(logn)`：

top()方法，访问队列中的队首元素，即优先级最高的元素：

pop()方法，取出队首元素，时间复杂度为`O(logn)`

```C++
#include <iostream>
#include <queue>

int main(){
    using namespace std;
    priority_queue<int> q;
    q.push(3);
    q.push(4);
    q.push(1);
    cout << q.top() << endl;
    q.pop();
    cout << q.top() << endl;
    return 0;
}
```

输出结果为：

`4`

`3`

empty()方法，用于判断队列是否为空，如果为空则返回true，否则返回false，时间复杂度为`O(1)`

```c++
#include <iostream>
#include <queue>

int main(){
    using namespace std;
    priority_queue<int> q;
    cout << q.empty() << endl;
    q.push(3);
    cout << q.empty() << endl;
    return 0;
}
```

输出结果为：

`1`

`0`

size()方法，返回队列中元素的个数，时间复杂度为`O(1)`：

```C++
#include <iostream>
#include <queue>

int main(){
    using namespace std;
    priority_queue<int> q;
    q.push(3);
    q.push(4);
    q.push(1);
    cout << q.size() << endl;
    return 0;
}
```

##### 设置元素的优先级

先看看对于基本类型的元素是如何设置优先级的。

###### 基本类型的优先级

假如创建一个int类型的优先队列，那么声明对象的语句为：

`priority_queue<int> q;`

但这实际上省略了两个默认参数，也就是说，这个语句的原型应该是：

`priority_queue<int, vector<int>, less<int> > q;`

其中，`vector<int>`是在底层承载堆结构的数组，而`less<int>`表示元素越大，优先级越高；对应的，这个参数还有一个可选的取值为`greater<int>`表示元素越小，优先级越高。

所以想将最小的数字设置为最高的优先级，可以这样定义一个优先队列：

```c++
#include <iostream>
#include <queue>

int main(){
    using namespace std;
    priority_queue<int, vector<int>, greater<int> > q;
    q.push(3);
    q.push(4);
    q.push(1);
    cout << q.top() << endl;
    return 0;
}
```

输出结果为：`1`

###### 结构体的优先级

如果要创建一个结构体类型元素的优先队列，那么需要对`<`运算符：

```c++
#include <iostream>
#include <queue>
#include <string>

struct fruit{
    int price;
    std::string name;
    friend bool operator < (fruit a, fruit b){
        return a.price < b.price;
    }
};

int main(){
    using namespace std;
    priority_queue<fruit> q;
    fruit a = {3, "apple"};
    fruit b = {4, "peach"};
    fruit c = {1, "orange"};
    q.push(a);
    q.push(b);
    q.push(c);
    cout << q.top().name << " " << q.top().price << endl;
    return 0;
}
```

需要注意的上面的操作符函数必须声明为友元。

输出结果为：`peach 4`

如果想将价格低的水果设置为最高优先级，可以修改重载`<`运算符的操作符函数的return语句：

```c++
#include <iostream>
#include <queue>
#include <string>

struct fruit{
    int price;
    std::string name;
    friend bool operator < (fruit a, fruit b){
        return a.price > b.price;
    }
};

int main(){
    using namespace std;
    priority_queue<fruit> q;
    fruit a = {3, "apple"};
    fruit b = {4, "peach"};
    fruit c = {1, "orange"};
    q.push(a);
    q.push(b);
    q.push(c);
    cout << q.top().name << " " << q.top().price << endl;
    return 0;
}
```

输出结果为：`orange 1`

除了上面那样将通过一个友元函数来重载`<`运算符的方式外，还有另一种通过在另一个结构体中重载`()`运算符来设置元素优先级的方式：

```c++
#include <iostream>
#include <queue>
#include <string>

struct fruit{
    int price;
    std::string name;
};

struct cmp{
    bool operator () (fruit a, fruit b){
        return a.price < b.price;
    }
};

int main(){
    using namespace std;
    priority_queue<fruit, vector<fruit>, cmp> q;
    fruit a = {3, "apple"};
    fruit b = {4, "peach"};
    fruit c = {1, "orange"};
    q.push(a);
    q.push(b);
    q.push(c);
    cout << q.top().name << " " << q.top().price << endl;
    return 0;
}
```

输出结果为：`peach 4`

从上面的实验结果可以看出，可以将priority_queue直接当成堆来使用，因为其底层就是通过堆来实现的。所以在需要借助堆数据结构实现某些算法时可以借助priority_queue来实现。

