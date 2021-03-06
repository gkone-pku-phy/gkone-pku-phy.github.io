<!-- slide -->
# 非线性谐振子 {.middle}
<br>
<br>

## 钱都 郭凯一 刘雨彤 王迟傲
## 2022/6/1

<!-- slide -->
# 1.简要概述与分析 {.top}
\content[]{
\question[问题概述]{
非线性谐振子的方程为：
$$
\ddot{x} +\omega_0^2x + A x^2 + B x^3 +\cdots = 0
$$
探究非线性谐振子运动情况。给出七阶修正。
分别取$c_i=1,c_j=0(j\ne i) (i=1,2,\cdots)$，与线性谐振子相比，非线性项如何破坏周期性行为?
}

加入非线性项之后，$x(t)$依然是一个周期函数，但振动的周期和函数形式不再是简单的简谐振动$\sin(\omega_0t),\cos(\omega_0t) $。但由于它还是周期函数（假设这个原频率为$\omega$），我们可以对它进行傅里叶级数展开:

$$
x(t)=\sum_{n=-\infty}^{\infty} f_n e^{in\omega t}
$$

其中$f_n$是各项的振幅。我们期望通过将其代入到方程中，求出$f_n$的值，从而解出运动形式
}

<!-- slide -->
# 2.$x^n$的计算与离散卷积 {.top}
\content[]{
\question[问题]{
我们有了$x(t)$的展开式，该如何计算并合并各阶非线性项中$x^n(t)$的值？这是计算的**核心问题**
}

$$
\begin{align*}
x(t)&=\sum_{n=-\infty}^{\infty} f_n e^{in\omega t}\\
x^2(t)&=\sum_{n=-\infty}^{\infty}\sum_{m-\infty}^{\infty} f_n f_m e^{i(n+m)\omega t}\\
&=\sum_{u=-\infty}^\infty\left(\sum_{n=-\infty}^{\infty} f_n f_{u-n}\right) e^{iu\omega t}\\
&= \sum_{u=-\infty}^\infty g_u e^{iu\omega t}
\end{align*}
$$
其中$g_u = (f*f)_u=\sum_{n=-\infty}^{\infty} f_n f_{u-n}$是序列$f_n$和自己的离散卷积。从上述计算中我们可以看到，有了$x(t)$的频谱，我们可以很方便地表示它的幂次$x^2(t)$的频谱，即便它是非线性项。
同理，$x^k(t)$的频谱就是$k$个序列$f_n$作离散卷积，结果与$f_n$一样，也构成一个无穷序列。下面我们展示一个离散卷积的计算示例。
}

<!-- slide -->
### 离散卷积 {.thm}
\content[]{
我们将以$f^{(0)}$为例，展示卷积的计算过程。由于频谱中各个分量的幅值都是复数，我们不妨取实数的特殊情况讨论。$f^{(0)}$的表达式为：
$$
f_1^{(0)} = a\\
f_{-1}^{(0)}=\overline a\\
$$
下图为$a=\overline{a}=1$的情形
}

![pic](./pics/1.png)
<!-- slide -->
\content[]{
计算$g=f^{(0)}*f^{(0)}$:
$$
g_0 =\sum_{n=-\infty}^{\infty} f_n^{(0)}f_{-n}^{(0)}= 2a\overline{a}\\
g_2=\sum_{n=-\infty}^{\infty} f_n^{(0)}f_{2-n}^{(0)}=a^2,\\
g_{-2}=\overline{a}^2\\
$$
对应频谱图如下：
}

![pic](./pics/2.png)
<!-- slide -->

\content[]{
在此基础上计算$h=f^{(0)}*f^{(0)} * f^{(0)}=g * f^{(0)}$:
$$
\begin{align*}
h_{3}&=\sum_{n=-\infty}^{\infty} g_n^{(0)}f_{3-n}^{(0)} = a^3,\\
h_{-3}&=\sum_{n=-\infty}^{\infty} g_n^{(0)}f_{-3-n}^{(0)} =\overline{a}^3\\
h_{\pm 1}&= 3a^2 \overline{a},3a\overline{a}^2\\
\end{align*}
$$
对应频谱图如下：
}

![pic](./pics/3.png)

<!-- slide -->
卷积计算可以不断地进行下去：
$$
(f^{(0)}*f^{(0)}*f^{(0)}*f^{(0)}):
$$
![pic](./pics/4.png)
......
\def[总结]{
可以看出，对同一个函数地频谱进行多次卷积，会使得频谱由低频区向两侧的高频区扩展开来。这也是非线性谐振子频谱中高频项的来源。
}

<!-- slide -->

# 3.具体计算 {.top}
### a.线性情形 {.thm}
\content[]{
当方程没有非线性项时：
$$
\ddot{x} +\omega_0^2x=0
$$
它的通解为：
$$
x(t)=a\sin(\omega_0 t)+b\cos(\omega_0 t) 
$$
或者写成复数形式：
$$
x(t)=f_{1}e^{i\omega_0 t}+f_{-1} e^{-i\omega_0 t}
$$
由于$x$是实数，所以$f_{1}=f_{-1}^*$
}

<!-- slide -->
### b.非线性情形：计算思路 {.thm}
\content[]{
当存在非线性项，且非线性项的能量远小于谐振子项时,我们假设它对$f_n$和$\omega$的影响也是很小的，所以可以写成：

$$
f_n = f_n^{(0)}+f_n^{(1)}+f_n^{(2)}+\cdots\\
\omega = \omega_0 +\omega_1 +\omega_2 +\cdots
$$
亦即，每增加一阶微扰，离散的频谱序列会叠加一个小量，同时各个峰的位置也会移动一个小量。
<p>
<img src="./pics/5.jpg" style="width:40%;float:right;">

把它们和非线性项代入方程：

$$
\ddot{x} +\omega_0^2x + A x^2 + B x^3 +\cdots = 0
$$
$
0=\f{\rm d^2}{dt^2}\sum_{n=-\infty}^{\infty} (f_n^{(0)}+f_n^{(1)}+f_n^{(2)}+\cdots)e^{in(\omega_0 +\omega_1 +\omega_2 +\cdots)t}+\omega_0^2\sum_{n=-\infty}^{\infty} (f_n^{(0)}+f_n^{(1)}+f_n^{(2)}+\cdots)e^{in(\omega_0 +\omega_1 +\omega_2 +\cdots)t}+A\sum_{n=-\infty}^{\infty} (f^{(0)}+f^{(1)}+f^{(2)}+\cdots)*(f^{(0)}+f^{(1)}+f^{(2)}+\cdots)_n e^{in(\omega_0 +\omega_1 +\omega_2 +\cdots)t}+B\sum_{n=-\infty}^{\infty}(f*f*f)_ne^{in(\omega_0 +\omega_1 +\omega_2 +\cdots)t}+\cdots
$
</p>
}
<!-- slide -->
\content[]{
以上式子可以简写成：
$$
\sum_{n=-\infty}^\infty (-n^2\omega^2 f_n+\omega_0^2f_n +A(f*f)_n+B(f*f*f)_n+\cdots)e^{in\omega t}=0
$$
左侧为傅里叶展开式，右边是零，由$e^{in\omega t}$的完备性知，左侧各项系数为0：
$$
-n^2\omega^2 f_n+\omega_0^2f_n +A(f*f)_n+B(f*f*f)_n+\cdots=0\qquad  n=0,\pm 1,\pm 2,\cdots
$$
$
-n^2(\omega_0 +\omega_1 +\omega_2 +\cdots)^2 (f_n^{(0)}+f_n^{(1)}+f_n^{(2)}+\cdots)+\omega_0^2 ( f_n^{(0)}+f_n^{(1)}+f_n^{(2)}+\cdots)+A\sum_{n=-\infty}^{\infty} (f^{(0)}+f^{(1)}+f^{(2)}+\cdots)*(f^{(0)}+f^{(1)}+f^{(2)}+\cdots)_n+\cdots=0
$

将上式按大小阶数展开，相同阶数和为零，得到方程：

$
\text{第零阶:}\quad(-n^2+1)\omega_0^2 f_n^{(0)}=0, n=0,\pm 1,\pm 2,\cdots
$

$
\text{第一阶:}\quad A(f^{(0)}*f^{(0)})_n +\omega_0^2f_n^{(1)}-2n^2 \omega_0 \omega_1 f_n^{(0)}-n^2 \omega_0 f_n^{(1)}=0, n=0,\pm 1,\pm 2,\cdots
$

}

<!-- slide -->
### 第零阶 {.thm}
\content[]{
$$
\quad(-n^2+1)\omega_0^2 f_n^{(0)}=0, n=0,\pm 1,\pm 2,\cdots
$$

从第零阶中可以解出
$$
\begin{cases}
f_n^{(0)}= 0,n\ne \pm 1\\
f_n^{(0)}\ne 0, n=\pm 1
\end{cases}
$$
由于$x(t)$为实数，$f_n=f_n^*$，不妨设$f_{ 1}^{(0)}=a,f_{ -1}^{(0)}=\overline{a}$
因此第零阶解对应$\f{1}{2}\omega_0^2x^2$的线性项：
$$
x(t)=2\rm{Re}(a) \cos \omega_0 t-2\rm{Im}(a) \sin \omega_0 t
$$

}
<!-- slide -->

### 第一阶 {.thm}
\content[]{
$$
\quad A(f^{(0)}*f^{(0)})_n +\omega_0^2f_n^{(1)}-2n^2 \omega_0 \omega_1 f_n^{(0)}-n^2 \omega_0 f_n^{(1)}=0, n=0,\pm 1,\pm 2,\cdots
$$

第一阶中含有$f_n^{(1)},\omega_1$两个未知量。
当$n=\pm 1$时，方程中$f_n^{(1)}$前系数为零，方程变为：
$$
\quad A(f^{(0)}*f^{(0)})_{\pm 1} -2 \omega_0 \omega_1 f_{\pm 1}^{(0)}=0
$$
方程中未知的只剩下$\omega_1$,可以解出：
$$
\omega_1 = \f{A(f^{(0)}*f^{(0)})_{\pm 1}}{2\omega_0 f_{\pm 1}^{0}}
$$
经过计算知,$\omega_1=0$.
当$n\ne \pm 1$时，代入$\omega_1=0$可以计算各个$f_n^{(1)}$的值：
$$
f_n^{(1)}=\f{A(f^{(0)}*f^{(0)})_n}{(n^2-1)\omega_0^2}\qquad (n\ne \pm 1)
$$
看起来我们无法计算$f_{\pm 1}^{(1)}$的值，但因为第零阶中的$a$是人为规定的，故可以包含高阶下$n=\pm 1$的微扰（相当于假设振动基频的振幅就是$a,\overline{a}$）
因此我们不妨设$f_{\pm 1}^{(1)}=0$
$$
f_0^{(1)}=- \frac{2 A_{1} a \overline{a}}{\omega_{0}^{2}},
f_{-2}^{(1)}=\frac{A_{1} \overline{a}^{2}}{3 \omega_{0}^{2}},
f_2^{(1)}=\frac{A_{1} a^{2}}{3 \omega_{0}^{2}}
$$
}

<!-- slide -->
### 更高阶的一般性分析 {.thm}
\content[]{
第$k$阶的方程可以写作：
$
(-n^2+1)\omega_0^2 f_n^{(k)}-2f_n^{(0)}n^2\omega_0 \omega_k +\lambda_n(\omega_0^2,A_1,\cdots,A_{k},\omega_1,\cdots,\omega_{k-1},f_n^{(0)},f_n^{(1)},\cdots,f_n^{(k-1)})=0
$
在求第$k$阶之前，我们已经求得了$\omega_1,\cdots,\omega_{k-1},f_n^{(0)},\cdots,f_n^{(k-1)}$的值，因此函数$\lambda_n$是已知项
- $n= \pm 1$ 可以求出$\omega_k$
- $n\ne \pm 1$可以求出$f_n^{(k)}(n\ne \pm 1)$
因此可以不断地计算下去。
}

<!-- slide -->

# 计算自动化 {.top}
\content[]{

可以看到，更高阶的计算十分繁琐，涉及的计算不仅项数极多，而且计算式中存在对无穷序列的多次离散卷积，很难处理。

为了减少计算量，我们转而使用自动化符号计算工具(sympy)，并开发了一个计算各阶项参数的[程序](./1.ipynb)，完成了前七阶微扰的求解。

当然，通过改变参数，我们也可以很快得到更高阶的微扰项。
由于更高阶的计算结果十分复杂，这里只展示 $ k\le 3$ 的微扰项（微扰频率和对应频谱）。读者若有兴趣，可以在[这里](./1.html)找到进行符号计算所用的程序代码，和零阶到七阶微扰的全部表达式。

}


<!-- slide -->
### 一些重要的结果: {.thm}
\content[]{
(下面设定$f_1^{(0)}=a,f_{-1}^{(0)}=\overline{a}$)
#### 第一阶：
$\omega_1=0$
$f_0^{(1)}=- \frac{2 A_{1} a \overline{a}}{\omega_{0}^{2}}$
$f_{2}^{(1)}=\frac{A_{1} a^{2}}{3 \omega_{0}^{2}},\qquad f_{-2}^{(1)}=\frac{A_{1} \overline{a}^{2}}{3 \omega_{0}^{2}}$
#### 第二阶：
$\omega_2=\frac{a \left(- 10 A_{1}^{2} + 9 A_{2} \omega_{0}^{2}\right) \overline{a}}{6 \omega_{0}^{3}}$
$f_{3}^{(2)}=\frac{A_{1}^{2} a^{3}}{12 \omega_{0}^{4}} + \frac{A_{2} a^{3}}{8 \omega_{0}^{2}},\qquad f_{-3}^{(2)}=\frac{A_{1}^{2} \overline{a}^{3}}{12 \omega_{0}^{4}} + \frac{A_{2} \overline{a}^{3}}{8 \omega_{0}^{2}}$
#### 第三阶：

$\omega_3=0$
$f_0^{(3)}=- \frac{38 A_{1}^{3} a^{2} \overline{a}^{2}}{9 \omega_{0}^{6}} + \frac{10 A_{1} A_{2} a^{2} \overline{a}^{2}}{\omega_{0}^{4}} - \frac{6 A_{3} a^{2} \overline{a}^{2}}{\omega_{0}^{2}}$
$f_{2}^{(3)}=\frac{59 A_{1}^{3} a^{3} \overline{a}}{54 \omega_{0}^{6}} - \frac{31 A_{1} A_{2} a^{3} \overline{a}}{12 \omega_{0}^{4}} + \frac{4 A_{3} a^{3} \overline{a}}{3 \omega_{0}^{2}},\qquad f_{-2}^{(3)}=\frac{59 A_{1}^{3} a \overline{a}^{3}}{54 \omega_{0}^{6}} - \frac{31 A_{1} A_{2} a \overline{a}^{3}}{12 \omega_{0}^{4}} + \frac{4 A_{3} a \overline{a}^{3}}{3 \omega_{0}^{2}}$
$f_{4}^{(3)}=\frac{A_{1}^{3} a^{4}}{54 \omega_{0}^{6}} + \frac{A_{1} A_{2} a^{4}}{12 \omega_{0}^{4}} + \frac{A_{3} a^{4}}{15 \omega_{0}^{2}},\qquad f_{-4}^{(3)}=\frac{A_{1}^{3} \overline{a}^{4}}{54 \omega_{0}^{6}} + \frac{A_{1} A_{2} \overline{a}^{4}}{12 \omega_{0}^{4}} + \frac{A_{3} \overline{a}^{4}}{15 \omega_{0}^{2}}$


}

<!-- slide -->
### 计算结果得出的规律 {.thm}
\content[]{
(查看[计算结果](./1.html))
- $\omega_{2k}\ne 0,\omega_{2k+1}=0$。

应当注意到，这是可以直观理解的：$2k+1$阶的作用力在简谐振子的两侧相互抵消，对于总体周期的变化无贡献；而$2k$阶的作用力在运动过程中始终指向/背离平衡点，这会减小/增大振子周期。
- 圆频率修正的大小和振幅**相关**：$\omega=\omega(a)$，而线性振子的圆频率和振幅**无关**。这是**非线性振子**所特有的性质。
- 阶数$k$与对应频谱修正项关系：
    - 共轭：$f_n^{(k)}=\overline{f_{-n}^{(k)}}$
    - k阶的频谱修正$f_n^{(k)}$只对有限个$n$不为0，且k越大不为零的数量越多
        - $k=1: n=0,\pm 2$
        - $k=2: n=\pm 3$
        - $k=3: n=0,\pm 2,\pm 4$
    - 奇偶性：当且仅当k为奇数时，存在对$f_0$（也就是平衡位置）的修正。这是因为谐振子该阶项对应的受力始终沿着一个方向；k为偶数时对$f_0$的修正为0
- 非线性项$A_i$对频谱修正的关系：
    - $A_k$对频谱的影响从第$k$阶开始出现，会出现无限多包含$A_k$的项
}

<!-- slide -->
# 第二部分：分别代入各$A_i=0$ {.top}
### 代入$A_1=1,\quad A_i=0(i\ge 2)$ {.thm}
\content[]{
- 对第零阶无影响
- 第一阶：
$$
\omega_1=0\\
f_0^{(1)}=-\f{2a\overline{a}}{\omega_0^2}\\
f_2^{(1)}=\f{a^2}{3\omega_0^2},\qquad f_{-2}^{(1)}=\f{\overline{a}^2}{3\omega_0^2}
$$
- 第二阶：
$$
\omega_2=\f{-5a\overline{a}}{3\omega_0^3}\\
f_{3}^{(2)}=\f{a^3}{12\omega_0^4},\qquad f_{-3}^{(2)}=\f{\overline{a}^3}{12\omega_0^4}\\
\cdots
$$
([更多结果](./1.html#%E4%BB%A3%E5%85%A5%E7%AC%AC1%E9%98%B6%EF%BC%9A$A_%7B1%7D=1,else=0$))
}
<!-- slide -->
### 一些特殊情形下的性质 {.thm}
\content[] {

- 不同$A_i$产生的频谱**不能叠加**（因为存在$A_1A_2$这样的非线性项）
- 当只有$A_i\ne 0$,$A_i$对各阶修正频率的影响：
    - $A_{2k}$只影响$\omega_{2k},\omega_{4k},\cdots$
    - $A_{2k+1}$只影响$\omega_{2(2k+1)},\omega_{4(2k+1)},\cdots$
- $A_i\ne 0$,$A_i$对各阶修正频谱的影响：
    - $A_{k}$对所有$f_n^{(k)}$,$f_n^{(2k)},\cdots$有影响
}
<!-- slide -->
# the end
# 感谢观看