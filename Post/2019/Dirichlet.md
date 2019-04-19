~~%%%进哥~~

笔记抄自进哥的pdf
### 预备知识
* gcd(x,y)为x,y的最大公约数,lcm(x,y)为x,y的最小公倍数
* [some_condition]当 some_condition为真时等于１，为假时等于０
* $\phi(n)$为欧拉函数，μ(n)为莫比乌斯函数
* σ(n) 为 n 的约数之和.
* $σ_k (n) 为 n 的约数的 k 次方之和.$
* 如果对于任意gcd(a,b)=1有f(ab)=f(a)*f(b),我们称f(n)为积性函数
* 如果对于任意f(ab)=f(a)*f(b),我们称f(n)为完全积性函数
* 数论函数:定义域为自然数，陪域为复数的函数
### Dirichlet 卷积
定义:对于数论函数f,g,定义其 狄利克雷卷积(f*g)(n)=      
 $$\sum_{d|n}{f(d)g(\frac{n}{d})}$$

运算
* **交换律: ```f * g=g * f```**

易证

* **结合率: ```(f*g)*h=f*(g*h)```**

证明:

$(f*g)*h(n)$

$=\sum_{n|k}{(\sum_{d|n}{f(d)g(\frac{n}{d})})h(\frac{k}{n})}$

$=\sum_{n|k}{\sum_{d|n}{f(d)g(\frac{n}{d})}h(\frac{k}{n})}$

$=\sum_{n|k}{\sum_{d|n}{f(\frac{k}{n})g(\frac{n}{d})}h(d)}$

$=\sum_{n|k}{(\sum_{d|n}{g(\frac{n}{d})}h(d))f(\frac{k}{n})}$

$=f*(g*h)$

* **分配率: ```f*(g+h)=f*g+f*h=(g+h)*f```**

证明:

$f*(g+h)(n)$

$=\sum_{d|n}{f(d|n)*[g(d)+h(d)]}$

$=\sum_{d|n}{f(\frac{n}{d})*g(d)}$+ 
$\sum_{d|n}{f(\frac{n}{d})*h(d)}$

=**```f*g+f*h```**

* **如果f,g均为积性函数，那么f*g也是积性函数。**

证明:
设$d_1d_2=d,n_1n_2=n,gcd(d_1,d_2)=1,gcd(n_1,n_2)=1$

$(f*g)(n)$

$=\sum_{d|n}{f(d)g(\frac{n}{d})}$

=$\sum_{d_1d_2|n}{f(d_1d_2)g(\frac{n}{d_1d_2})}$

=$\sum_{d_1d_2|n}{f(d_1)f(d_2)g(\frac{n_1}{d_1})g(\frac{n_2}{d_2})}$

=$\sum_{d_1d_2|n_1n_2}{f(d_1)g(\frac{n_1}{d_1})f(d_2)g(\frac{n_2}{d_2})}$

=$(f*g)(n_1)*(f*g)(n_2)$

* [ x ] [Bash Plays with Functions](https://www.luogu.org/problemnew/show/CF757E)
