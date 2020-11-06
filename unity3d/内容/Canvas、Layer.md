# Canvas、Layer

#### Render Mode

##### Screen Space -OverLay

- Canvas会被缩放以适应屏幕，然后直接渲染到屏幕上，无需任何摄像机（即使当前Scene中没有任何摄像机）。
- UI会覆盖所有其他摄像机所见的画面。

##### Screen Space-Camera

- UI在屏幕上的大小并不随此距离变化而变化。
- Scene中任何比UI平面距离摄像机更近的3D物件，都将先于UI被渲染。
- 相反位于UI平面后面的物件就会被遮挡。

##### World Space

- UI被看作是Scene中的一个平面物件。
- 通过RectTransform可以设置Canvas尺寸，但他的屏幕大小将取决于摄像机的视角以及距离。



参考：

https://gameinstitute.qq.com/community/detail/112504

https://www.shangmayuan.com/a/3a814ab1d2b949abae2a330b.html