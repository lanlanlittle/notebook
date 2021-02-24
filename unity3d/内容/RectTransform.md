# RectTransform

#### 一、概念

##### Anchor

锚点 anchorMax==anchorMin（绝对布局）

锚框 (相对布局)

##### Pivot

##### Offset

##### sizeDelta

> **所以这个属性之所以叫做sizeDelta，是因为在锚点情况下其表征的是size（大小），在锚框的情况下其表征的是Delta（差值）**

##### anchoredPosition

> 在使用`锚点`的情况下，anchoredPosition表征的是元素Pivot到Anchor的距离
>
> 在使用`锚框`的情况下，anchoredPosition表征的是元素Pivot到锚框中心点的距离



#### 二、api

##### 1、SetSizeWithCurrentAnchors(Animations.Axis axis, float size)

这个方法无论在`绝对布局`还是`相对布局`的情况下，都可以通过直接设置rect中的`width`和`height`值来改变UI元素的大小。

##### 2、SetInsetAndSizeFromParentEdge([RectTransform.Edge](https://links.jianshu.com/go?to=https%3A%2F%2Fdocs.unity3d.com%2FScriptReference%2FRectTransform.Edge.html) edge, float inset, float size)

在使用这个方法的时候要注意锚点也会改变，改变的规则为

- 以左边界为基准时，`anchorMin`和`anchorMax` 的`y`不变`x`变为0.
- 以右边界为基准时，`anchorMin`和`anchorMax` 的`y`不变`x`变为1.
- 以上边界为基准时，`anchorMin`和`anchorMax` 的`x`不变`y`变为1.
- 以下边界为基准时，`anchorMin`和`anchorMax` 的`x`不变`y`变为0.

##### 3、GetWorldCorners(Vector3[] fourCornersArray)

使用这个方法，可以取得UI元素四个角的世界坐标，具体使用方法，先建立一个长度为4的vector3数组，然后传进这个方法，调用一次后，数组被赋值，里面的四个元素分别是UI的`左下角` ，`左上角`，`右上角`，`右下角`。

参考：

https://www.jianshu.com/p/4592bf809c8b

