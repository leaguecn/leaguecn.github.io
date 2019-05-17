---
title: 招聘笔试编程题笔记
date: 2019-05-17 01:50:30
tags:
- 工作
- 招聘
- 编程笔记
- work
- recruit
- coding note
categories:
- 工作
---

+ 首先声明一下，本人很懒，然后博客搭建了之后，就较少更新博客了，原因有几个；

    + 原因1：临近毕业了，论文|工作各种忙，所以很少时间整理知识点；
    + 原因2：一直没有idea，要写什么博客，是技术编程，还是鸡汤美文，还没想好；
    + 原因3：比较懒，对我就是那种死肥宅的一类人物，博客更新看心情吧；
    + 原因4：其实写一些意义不大的吐槽的，或结构不完整的博客，本人觉得还不如不写。
<!--More -->

+ 之前在应聘各种单位|公司，虽然不是什么CS科班出身，但是难免会遇上一些装X的公司想试试你的编程能力
从此他们开始走向一条不归路。然后想把这些暂存在脑海里的编程题记录下来，归档或给后来者提供一些参考
毕竟现在，乐意在网上分享知识经验的人还是少数的，而能分享一些有意义的知识更是寥寥无几。

+ 以上是起因，下文进入正题。

*特别声明：限于本人知识水平有限，本文可能存在一些不足，还请谅解!*

## 编程题

### 公司1

+ 判断平面点在指定的直线的左边还是右边

```
题目重述：
给定点A(xa, ya)和点B(xb, yb)，A、B两点确定了一条直线；
然后，假定需要判定的点C坐标为(xc, yc)，如何判定C点相对于AB直线位置；
请编程实现判定点C相对于直线AB的位置，左边返回true，右边返回false。

解题思路：
利用向量叉乘的正负判定其位于直线左边还是右边。
```

+ C++ 编程实现

```
// judge a point in which side of one line consisted with tow line in plane
// @author ligurecn
// xuzhou, 2019.03.19
#include <iostream>
#include <ctime>
#include <cstdlib>
#include <time.h>

using namespace std;

double random(double start, double end){
    return start+(end-start)*rand()/(RAND_MAX + 1.0);
}
bool getJudgement(double point[], double line[2][2]){
    //reconstruct vertors like a, b
    // then use cross product method to judge
    // if result is positive, point in left, otherwise negetive, point in right
    bool isLeft=false;
    double a[2], b[2];
    for(int i=0; i<2; i++)
        a[i] = line[1][i]-line[0][i], b[i]=point[i]-line[0][i];

    double res = a[0] * b[1] - a[1] * b[0];
    if(res > 0) isLeft = true;
    return isLeft;
}

int main(){
    double line[2][2];
    double point[2];

    srand(int(time(0)));//seed from time
    for (int i = 0; i < 2; i++) {
        for(int j=0; j<2; j++)line[i][j] = random(-10, 10);
        point[i] = random(-10, 10);
    }

    // judge point position in which side of line
    // if in left side, return true
    // in right side, return false
    bool isLeft = getJudgement(point, line);
    cout << "- point(" << point[0] << ", " << point[1]<< ")\n";
    if(isLeft) cout << "-> in left side of line: ";
    else cout << "-> right side of line: ";

    cout << "(" << line[0][0] << "," << line[0][1] << ")<->"
         << "(" << line[1][0] << "," << line[1][1] << ")\n";

    return 0;
}

```


+ 测试结果

```
//编译
$ g++ lrj.cpp -o pp
///////////////////////////Test 1
$ ./pp
- point(-6.2113, 8.92874)
-> in left side of line: (0.0824081,9.7702)<->(-5.83127,9.57272)
///////////////////////////Test 2
$ ./pp
- point(8.20822, 8.60886)
-> right side of line: (4.5333,-5.9355)<->(-8.27962,-2.37346)
///////////////////////////Test 3
$ ./pp
- point(-1.58741, 0.621722)
-> right side of line: (0.306838,-4.67183)<->(-6.34671,0.975676)
```

---


+ 求向量元素前n个之和值为最大、最小时的位置。

```
题目重述：
给定一组向量V(1, -9, 30, 3, -20, 9, ..., 88)；
前n个元素之和为：1+(-9)+30=22，但22不一定是最大或最小；
请编程实现找出前n个元素最大和最小值的位置。

解题思路：
遍历将向量的前n个元素之和依次计算，然后找出最大、最小值，最后根据index给出位置即可。
```

+ C++编程实现


```
// sum test
// @author ligurecn
// xuzhou, 2019-03-18
#include <iostream>
#include <ctime>
#include <cstdlib>
#include <time.h>

using namespace std;

double random(double start, double end){
    return start+(end-start)*rand()/(RAND_MAX + 1.0);
}
int minv(int v[], int len){
    int mn = v[0];
    for(int i=0; i<len; i++){
        if (v[i]<mn) mn = v[i];
    }
    return mn;
}
int maxv(int v[], int len){
    int mx= v[0];
    for(int i=0; i<len; i++){
        if(v[i]>mx) mx = v[i];
    }
    return mx;
}

int main(int argc, char** argv){
    // tips of using.
    if(argc < 2){
        cout << "- Usage: " << argv[0] << " Num" << endl;
    }
    // get the num para.
    int num = atoi(argv[1]);
    // initial array: V.
    int V[num];
    // seed random number via unix time var.
    srand((int)time(0));
    // generate the array via random function.
    for (int i=0; i< num; i++) V[i] = int(random(-50, 50));
    // then display them.
    cout << "- Original array:\n";
    for (int i=0; i< num; i++) cout << V[i] << " ";
    cout << endl;
    // get sum of first N int var in V.
    int S[num];
    for (int i=0; i< num; i++) {
        if(i==0) S[i]=V[i];
        else S[i]=S[i-1]+V[i];
    }
    // see the array of sum.
    cout << "Sum array:\n";
    for (int i=0; i< num; i++) cout << S[i] << " ";
    cout << endl;
    // pick out the min & max value of sum array.
    int mins = minv(S, num);
    int maxs = maxv(S, num);
    int mins_idx, maxs_idx;
    // fetch min & max index via their value.
    // perhaps, there are more than one of them.
    for (int i=0; i< num; i++){
        if(S[i]==mins) mins_idx = i;
        if(S[i]==maxs) maxs_idx = i;
    }
    // show the final answer.
    cout << "-> min sum value is: " << mins
        << ", in position: " << mins_idx+1 << endl;
    cout << "-> max sum value is: " << maxs
        << ", in position: " << maxs_idx+1 << endl;
    return 0;
}
```


+ 测试结果

```
// 编译
$g++ test.cpp -o test
/////////////////////////////1
$./test 10
- Original array:
20 -11 47 -36 24 45 6 46 -44 -5
Sum array:
20 9 56 20 44 89 95 141 97 92
-> min sum value is: 9, in position: 2
-> max sum value is: 141, in position: 8
/////////////////////////////2
$ ./test 15
- Original array:
25 -15 6 -16 -6 -31 -29 -21 24 -9 28 14 -3 -46 35
Sum array:
25 10 16 0 -6 -37 -66 -87 -63 -72 -44 -30 -33 -79 -44
-> min sum value is: -87, in position: 8
-> max sum value is: 25, in position: 1
/////////////////////////////3
$ ./test 20
- Original array:
13 -6 -27 -12 48 -45 -35 28 -3 26 49 20 29 17 -32 -31 36 28 1 31
Sum array:
13 7 -20 -32 16 -29 -64 -36 -39 -13 36 56 85 102 70 39 75 103 104 135
-> min sum value is: -64, in position: 7
-> max sum value is: 135, in position: 20
```

## 参考资料
+ https://dev.gameres.com/Program/Abstract/Geometry.htm#%E5%88%A4%E6%96%AD%E7%82%B9%E6%98%AF%E5%90%A6%E5%9C%A8%E7%BA%BF%E6%AE%B5%E4%B8%8A
+ http://www.cnblogs.com/carekee/articles/2299546.html
