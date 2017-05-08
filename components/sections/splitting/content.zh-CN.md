# 分割曲线

通过de Casteljau算法，我们还能找到将贝塞尔曲线分成两部分所需要的所有点，这两段小的部分组成了原来的那条曲线。当我们为某些`t`值构造de Casteljau骨架时，可以得到我们在`t`处分割曲线所需要的所有点：一条曲线由该曲线点之前的所有骨架点定义，另一条则由曲线点之后的所有骨架点定义。

<Graphic title="分割一条曲线" setup={this.setupCubic} draw={this.drawSplit} />

<div className="howtocode">

### 实现曲线分割

我们可以在de Casteljau函数中添加一些额外的代码来实现曲线分割：

```
left=[]
right=[]
function drawCurve(points[], t):
  if(points.length==1):
    left.add(points[0])
    right.add(points[0])
    draw(points[0])
  else:
    newpoints=array(points.size-1)
    for(i=0; i<newpoints.length; i++):
      if(i==0):
        left.add(points[i])
      if(i==newpoints.length-1):
        right.add(points[i+1])
      newpoints[i] = (1-t) * points[i] + t * points[i+1]
    drawCurve(newpoints, t)
```

在对一些`t`值执行这个函数之后，数组`left`和`right`包含了两条新曲线的所有点坐标 - 一个是`t`值的“左边”，另外一个是“右边”，它们与原始曲线的顺序一样，并且完全覆盖于其上。

</div>

这是一个绝佳的动画图示（点击播放/暂停）：

<Graphic preset="threepanel" title="分割Bézier曲线" setup={this.setupCubic} draw={this.drawAnimated} onClick={this.togglePlay} />
