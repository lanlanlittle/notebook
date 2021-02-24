# AssetBundle

#### 压缩方式

- LZMA:BuildAssetBundleOptions.None

- LZ4:BuildAssetBundleOptions.ChunkBasedCompression

- 不压缩:BuildAssetBundleOptions.UncompressedAssetBundle

  

#### 读取/加载

AB加载方式：

1. AssetBundle.LoadFromFile 从本地加载

2. AssetBundle.LoadFromMemory 从内存加载

3. AssetBundle.LoadFromStream 从流加载

4. WWW.LoadFromCacheOrDownload 下载后放在缓存中备用(该方法逐渐被弃用)

5. UnityWebRequest 从服务器下载

   

从AB中加载资源：

1. AssetBundle.LoadAsset(assetName)
2. AssetBundle.LoadAllAssets() 加载AB包中所有的对象，不包含依赖的包
3. AssetBundle.LoadAssetAsync() 异步加载，加载较大资源的时候
4. AssetBundle.LoadAllAssetsAsync() 异步加载全部资源
5. AssetBundle.LoadAssetWithSubAssets 加载资源及其子资源



AssetBundle Variants

> AssetBundle Variants是Unity5的新特性。你可以将两组不同的资源指定为同一个AssetBundle但是指定不同的Variants，这样，你可以根据平台的不同加载不同的资源（例如支持高清资源的设备加载hd的Variants，不支持高清资源的设备加载sd的Variants）。可是使用[AssetImporter.assetBundleVariant](https://docs.unity3d.com/ScriptReference/AssetImporter-assetBundleVariant.html)设置Variants。



代码构建





https://zhuanlan.zhihu.com/p/93199562

https://blog.csdn.net/qq_35361471/article/details/82854560

AssetBundle打包浏览工具-https://github.com/Unity-Technologies/AssetBundles-Browser

assetbundle读取加载-https://www.cnblogs.com/chinarbolg/p/9601380.html

LZMA压缩文件与解压文件-http://www.xuanyusong.com/archives/3095

资源包的压缩-https://blog.csdn.net/u011926026/article/details/70155178?utm_medium=distribute.pc_aggpage_search_result.none-task-blog-2~all~baidu_landing_v2~default-1-70155178.nonecase

LZMA源码-https://sourceforge.net/projects/sevenzip/files/LZMA%20SDK/

LZ4源码-https://github.com/lz4/lz4

WWW.LoadFromCacheOrDownload-https://blog.csdn.net/zhjzhjxzhl/article/details/79743225

AssetImporter-https://zhuanlan.zhihu.com/p/39994056

AssetBundle Variants-[https://thistgg.github.io/2017/03/27/Unity5新的AssetBundle机制01——构建/](https://thistgg.github.io/2017/03/27/Unity5新的AssetBundle机制01——构建/)

AssetBundle 不能同名称-https://www.cnblogs.com/chongxin/p/5562469.html

热更原理-https://www.cnblogs.com/imteach/p/11257275.html

https://www.it610.com/article/1291775204829241344.htm



https://www.cnblogs.com/julyedu/p/11425443.html



https://blog.csdn.net/huangyimo/article/details/82980364



https://www.cnblogs.com/wuwenbo/p/7813246.html



https://blog.csdn.net/zgl159040290/article/details/52806507



http://www.xuanyusong.com/archives/3095