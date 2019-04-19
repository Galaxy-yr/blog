[BZOJ3207](https://www.lydsy.com/JudgeOnline/problem.php?id=3207)
## 花神的嘲讽计划Ⅰ

**背景**

花神是神，一大癖好就是嘲讽大J，举例如下：

“哎你傻不傻的！【hqz：大笨J】”

“这道题又被J屎过了！！”

“J这程序怎么跑这么快！J要逆袭了！”

……

**描述**

这一天DJ在给吾等众蒟蒻讲题，花神在一边做题无聊，就跑到了一边跟吾等众蒟蒻一起听。以下是部分摘录：

1.

“J你在讲什么！”

“我在讲XXX！”

“哎你傻不傻的！这么麻烦，直接XXX再XXX就好了！”

“……”

2.

“J你XXX讲过了没？”

“……”

“那个都不讲你就讲这个了？哎你傻不傻的！”

“……”

DJ对这种情景表示非常无语，每每出现这种情况，DJ都是非常尴尬的。

经过众蒟蒻研究，DJ在讲课之前会有一个长度为N方案，我们可以把它看作一个数列；

同样，花神在听课之前也会有一个嘲讽方案，有M个，每次会在x到y的这段时间开始嘲讽，为了减少题目难度，每次嘲讽方案的长度是一定的，为K。

花神嘲讽DJ让DJ尴尬需要的条件：

在x~y的时间内DJ没有讲到花神的嘲讽方案，即J的讲课方案中的x~y没有花神的嘲讽方案【这样花神会嘲讽J不会所以不讲】。

经过众蒟蒻努力，在一次讲课之前得到了花神嘲讽的各次方案，DJ得知了这个消息以后欣喜不已，DJ想知道花神的每次嘲讽是否会让DJ尴尬【说不出话来】。

## Input

第1行3个数N，M，K；

第2行N个数，意义如上；

第3行到第3+M-1行，每行K+2个数，前两个数为x,y,然后K个数，意义如上；

## Output

对于每一个嘲讽做出一个回答会尴尬输出‘Yes’，否则输出‘No’

**Sample Input**

8 5 3

1 2 3 4 5 6 7 8

2 5 2 3 4

1 8 3 2 1

5 7 4 5 6

2 5 1 2 3

1 7 3 4 5

**Sample Output**

No

Yes

Yes

Yes

No

## Solution

这道题我是打算写一下主席树的题目才看到的。写了一下发现不需要主席树，直接每k个hash一下，再sort一遍，
然后直接二分匹配就行了。

跑的还是挺快的。

![AC](https://i.loli.net/2019/04/13/5cb182cb70e0c.png)

代码

```cpp
/*******************************
Author:galaxy yr
LANG:C++
Created Time:2019年04月11日 星期四 17时01分12秒
*******************************/
#include<iostream>
#include<cstdio>
#include<algorithm>
using namespace std;
const int maxn=2e5+10;
const int base=131;
int n,m,k,a[maxn],cnt,val;
unsigned long long H[maxn];

struct hashmap{
    unsigned long long key;
    int rk;
    friend bool operator<(hashmap s,hashmap t) { return s.key<t.key; }
}e[maxn],h;

int main()
{
        freopen("bzoj3207.in","r",stdin);
        freopen("bzoj3207.out","w",stdout);
        scanf("%d%d%d",&n,&m,&k);
        for(int i=1;i<=n;i++)
            scanf("%d",&a[i]);
        for(int i=1;i<=n;i++)
            H[i]=H[i-1]*base+a[i];
        unsigned long long M=1;
        for(int i=1;i<=k;i++)
            M*=base;
        for(int i=k;i<=n;i++)
            e[++cnt].key=H[i]-H[i-k]*M,e[cnt].rk=i-k+1;
        sort(e+1,e+cnt);
        int l,r,z,y;
        while(m--)
        {
            scanf("%d%d",&l,&r);
            h.key=0;
            for(int i=1;i<=k;i++)
            {
                scanf("%d",&val);
                h.key=h.key*base+val;
            }
            z=lower_bound(e+1,e+cnt,h)-e;
            y=upper_bound(e+1,e+cnt,h)-e-1;
            if(z<=y)
            {
                if(e[z].rk>=l and e[z].rk<=r-k+1)
                    printf("No\n");
                else if(e[z].rk<l)
                {
                    if(e[y].rk>l)
                        printf("No\n");
                    else 
                        printf("Yes\n");
                }
                else 
                    printf("Yes\n");
            }
            else 
                printf("Yes\n");
        }
        return 0;
}
```
