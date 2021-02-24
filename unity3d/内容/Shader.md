# shader

#### Shader

Shader(着色器)：是可以在GPU上运行的一段程序，通过Shader可以进行一些渲染相关的设置。



#### ShaderLab

目前面向GPU的编程有三种高级图像语言：HLSL语言，GLSL语言，Cg语言。

- HLSL语言：High Level Shading Language，由Microsoft公司提供，通过Direct3D图形软件库来编写的着色器语言。
- GLSL语言：OpenGL Shading Language，由OpenGL安委会提供，在OpenGL中进行着色器编程的语言。
- Cg语言：C for Graphics，由NVIDIA公司和Microsoft公司合作提供，有自己的一套关键字和函数库，独立于三维编程接口，在Direct3D和OpenGL上都可工作。



**ShaderLab: Unity 自己又封装了一层CG/HLSL/GLSL的接口，但为了实现跨平台，Unity重点支持Cg着色器语言。**



#### Shader模版

- Standard Surface Shader

  标准表面着色器，是一种基于物理的着色系统（使用了Physically Based Rendering（简称PBR）技术，即基于物理的渲染技术），以模拟现实真实的方式来模拟材质与灯光之间的关系，可以很轻易的表现出各种金属反光效果，同时此种Shader的书写逻辑也更符合人类的思维模式。

- Unlit Shader

  Vertex/Fragment Shader,也就是最基本的顶点片断着色器，不受光照影响的Shader，多用于特效、UI上的效果制作。

- Image Effect Shader

  也是顶点片断着色器，只不过是针对后处理而定制的模版，后处理是什么呢？Bloom（也有人叫Glow/泛光/辉光等说法）、调色、景深、模糊等，这些基于最终整个屏幕画面而进行再处理的Shader就是后处理。

- Compute Shader

  Compute Shader是运行在图形显卡上的一段程序，独立于常规渲染管线之外的，它可以直接将GPU作为并行处理器加以利用，从而使GPU不仅具有3D渲染能力，还具有其他的运算能力。

- Shader Variant Collection

  Shader变体收集器，在上面创建的时候，你会发现Shader Variant Collection与以上四个是被隔开的，就是因为这个与它们不一样，它不是制作Shader的模版,而只是对Shader变体进行打包用的容器。

  > 注：以上的Standard Surface Shader、Unlit Shader、Image Effect Shader仅仅只是Unity为了方便我们书写而内置的几个模版，你完全可以建一个Unlit Shader，然后将其改成Surface Shader,同样也可以将一个Standard Surface Shader改成顶点片断着色器，所以这一点一定要明白，它们只是内容格式不一样的模版本而已，我们完全可以自由修改成任意我们想要的一种着色器类型，当然我们也可以通过一些手段来定制出我们自己的模版，这在后续章节中我们再进行详细介绍。



#### 材质与Shader的关系

1. 一个Shader可以与无数个材质关联。

2. 一个材质同一时刻只能关联于一个Shader。




shadertoy-https://www.shadertoy.com

unity shader官方文档-http://docs.unity3d.com/Documentation/Components/SL-SurfaceShaderLighting.html



参考：

http://www.cnblogs.com/tim-unity/p/4728274.html

https://www.cnblogs.com/Jason-c/p/8385946.html

https://www.zhihu.com/column/unityTA

Amplify Shader Editor-https://gameinstitute.qq.com/community/detail/112860

Unity Shader语法大全参考工具-https://github.com/taecg/ShaderReference

写Shader的IDE工具合集-https://zhuanlan.zhihu.com/p/147176392