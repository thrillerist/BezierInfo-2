# 贝塞尔曲线的数学原理

贝塞尔曲线是“参数”方程的一种形式。从数学上讲，参数方程作弊了：“方程”实际上是一个从输入到<strong>唯一</strong>输出的、良好定义的映射关系。几个输入进来，一个输出返回。改变输入变量，还是只有一个输出值。参数方程在这里作弊了。它们基本上干了这么件事，“好吧，我们想要更多的输出值，所以我们用了多个方程”。举个例子：假如我们有一个方程，通过一些计算，将假设为<i>x</i>的一些值映射到另外的值:

\[
  f(x) = \cos(x)
\]

记号<i>f(x)</i>是表示函数的标准方式（为了方便起见，如果只有一个的话，我们称函数为<i>f</i>），函数的输出根据一个变量（本例中是<i>x</i>）变化。改变<i>x</i>，<i>f(x)</i>的输出值也会变。

到目前没什么问题。现在，让我们来看一下参数方程，以及它们是怎么作弊的。我们取以下两个方程：

\[
\begin{matrix}
  f(a) = \cos(a) \\
  f(b) = \sin(b)
\end{matrix}
\]

这俩方程没什么让人印象深刻的，只不过是正弦函数和余弦函数，但正如你所见，输入变量有两个不同的名字。如果我们改变了<i>a</i>的值，<i>f(b)</i>的输出不会有变化，因为这个方程没有用到<i>a</i>。参数方程通过改变这点来作弊。在参数方程中，所有不同的方程共用一个变量，如下所示：

\[
\left \{ \begin{matrix}
  f_a(t) = \cos(t) \\
  f_b(t) = \sin(t)
\end{matrix} \right.
\]

多个方程，但只有一个变量。如果我们改变了<i>t</i>的值，<i>f<sub>a</sub>(t)</i>和<i>f<sub>b</sub>(t)</i>的输出都会发生变化。你可能会好奇这有什么用，答案其实很简单：对于参数曲线，如果我们用常用的标记来替代<i>f<sub>a</sub>(t)</i>和<i>f<sub>b</sub>(t)</i>，看起来就有些明朗了：

\[
\left \{ \begin{matrix}
  x = \cos(t) \\
  y = \sin(t)
\end{matrix} \right.
\]

好了，通过一些神秘的<i>t</i>值将<i>x</i>/<i>y</i>坐标系联系起来。

所以，参数曲线不像一般函数那样，通过<i>x</i>坐标来定义<i>y</i>坐标，而是用一个“控制”变量将它们连接起来。如果改变<i>t</i>的值，每次变化时我们都能得到<strong>两个</strong>值，这可以作为图形中的(<i>x</i>,<i>y</i>)坐标。比如上面的方程组，生成位于一个圆上的点：我们可以使<i>t</i>在正负极值间变化，得到的输出(<i>x</i>,<i>y</i>)都会位于一个以原点(0,0)为中心且半径为1的圆上。如果我们画出<i>t</i>从0到5时的值，将得到如下图像（你可以用上下键来改变画的点和值）：

<Graphic preset="empty" title="(一部分的)圆: x=sin(t), y=cos(t)" static={true} setup={this.setup} draw={this.draw} onKeyDown={this.props.onKeyDown}/>

贝塞尔曲线是（一种）参数方程，并在它的多个维度上使用相同的基本方程。在上述的例子中<i>x</i>值和<i>y</i>值使用了不同的方程，与此不同的是，贝塞尔曲线的<i>x</i>和<i>y</i>都用了“二项多项式”。那什么是二项多项式呢？

你可能记得高中所学的多项式，看起来像这样：

\[
  f(x) = a \cdot x^3 + b \cdot x^2 + c \cdot x + d
\]

如果它的最高次项是<i>x³</i>就称为“三次”多项式，如果最高次项是<i>x²</i>，称为“二次”多项式，如果只含有<i>x</i>的项，它就是一条线（不过不含任何<i>x</i>的项它就不是一个多项式！）

贝塞尔曲线不是x的多项式，它是<i>t</i>的多项式，<i>t</i>的值被限制在0和1之间，并且含有<i>a</i>，<i>b</i>等参数。它采用了二次项的形式，听起来很神奇但实际上就是混合不同值的简单描述：

\[
\begin{aligned}
  linear &= (1-t) + t \\
  square &= (1-t)^2 + 2 \cdot (1-t) \cdot t + t^2 \\
  cubic &= (1-t)^3 + 3 \cdot (1-t)^2 \cdot t + 3 \cdot (1-t) \cdot t^2 + t^3
\end{aligned}
\]

我明白你在想什么：这看起来并不简单，但如果我们拿掉<i>t</i>并让系数乘以1，事情就会立马简单很多，看看这些二次项：

\[
\begin{aligned}
  linear &= \hspace{2.5em} 1 + 1 \\
  square &= \hspace{1.7em} 1 + 2 + 1\\
  cubic &= \hspace{0.85em} 1 + 3 + 3 + 1\\
  hypercubic &= 1 + 4 + 6 + 4 + 1
\end{aligned}
\]

需要注意的是，2与1+1相同，3相当于2+1或1+2，6相当于3+3...如你所见，每次我们增加一个维度，只要简单地将头尾置为1，中间的操作都是“将上面的两个数字相加”。现在就能很容易地记住了。

还有一个简单的办法可以弄清参数项怎么工作的：如果我们将<i>(1-t)</i>重命名为<i>a</i>，将<i>t</i>重命名为<i>b</i>，暂时把权重删掉，可以得到这个：

\[
\begin{aligned}
  linear &= BLUE[a] + RED[b] \\
  square &= BLUE[a] \cdot BLUE[a] + BLUE[a] \cdot RED[b] + RED[b] \cdot RED[b] \\
  cubic &= BLUE[a] \cdot BLUE[a] \cdot BLUE[a] + BLUE[a] \cdot BLUE[a] \cdot RED[b] + BLUE[a] \cdot RED[b] \cdot RED[b] + RED[b] \cdot RED[b] \cdot RED[b]\\
\end{aligned}
\]

基本上它就是“每个<i>a</i>和<i>b</i>结合项”的和，在每个加号后面逐步的将<i>a</i>换成<i>b</i>。因此这也很简单。现在你已经知道了二次多项式，为了叙述的完整性，我将给出一般方程：

\[
  Bézier(n,t) = \sum_{i=0}^{n}
                \underset{binomial\ term}{\underbrace{\binom{n}{i}}}
                \cdot\
                \underset{polynomial\ term}{\underbrace{(1-t)^{n-i} \cdot t^{i}}}
\]

这就是贝塞尔曲线完整的描述。在这个函数中的Σ表示了这是一系列的加法（用Σ下面的变量，从...=<值>开始，直到Σ上面的数字结束）。

<div className="howtocode">

### 如何实现基本方程

我们可以用之前说过的方程，来简单地实现基本方程作为数学构造，如下：

```
function Bezier(n,t):
  sum = 0
  for(k=0; k<n; k++):
    sum += n!/(k!*(n-k)!) * (1-t)^(n-k) * t^(k)
  return sum
```

我说我们“可以用”是因为我们不会这么去做：因为阶乘函数开销*非常大*。并且，正如我们在上面所看到的，我们不用阶乘也能够很容易地构造出帕斯卡三角形：一开始是[1]，接着是[1,2,1],然后是[1,3,3,1]等等。下一行都比上一行多一个数，首尾都为1，中间的数字是上一行两边元素的和。

我们可以很快的生成这个列表，并在之后使用这个查找表而不用再计算二次多项式的系数：

```
lut = [      [1],           // n=0
            [1,1],          // n=1
           [1,2,1],         // n=2
          [1,3,3,1],        // n=3
         [1,4,6,4,1],       // n=4
        [1,5,10,10,5,1],    // n=5
       [1,6,15,20,15,6,1]]  // n=6

binomial(n,k):
  while(n >= lut.length):
    s = lut.length
    nextRow = new array(size=s+1)
    nextRow[0] = 1
    for(i=1, prev=s-1; i<prev; i++):
      nextRow[i] = lut[prev][i-1] + lut[prev][i]
    nextRow[s] = 1
    lut.add(nextRow)
  return lut[n][k]
```

这里做了些什么？首先，我们声明了一个足够大的查找表。然后，我们声明了一个函数来获取我们想要的值，并且确保当一个请求的n/k对不在LUT查找表中时，先将表扩大。我们的基本函数如下所示：

```
function Bezier(n,t):
  sum = 0
  for(k=0; k<=n; k++):
    sum += binomial(n,k) * (1-t)^(n-k) * t^(k)
  return sum
```

完美。当然我们可以进一步优化。为了大部分的计算机图形学目的，我们不需要任意的曲线。我们需要二次曲线和三次曲线（实际上这篇文章没有涉及任意次的曲线，因此你会在其他地方看到与这些类似的代码），这说明我们可以彻底简化代码:

```
function Bezier(2,t):
  t2 = t * t
  mt = 1-t
  mt2 = mt * mt
  return mt2 + 2*mt*t + t2

function Bezier(3,t):
  t2 = t * t
  t3 = t2 * t
  mt = 1-t
  mt2 = mt * mt
  mt3 = mt2 * mt
  return mt3 + 3*mt2*t + 3*mt*t2 + t3
```

现在我们知道如何代用码实现基本方程了。很好。

</div>

既然我们已经知道基本函数的样子，是时候添加一些魔法来使贝塞尔曲线变得特殊了：控制点。
