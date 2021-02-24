





Unity路径

- Application.dataPaht : (只读)应用程序安装目录 

- Application.streamingAssetsPath:(只读)应用程序asset目录

  ​	这是一个只读、不可写的目录。

  ​	unity说明：https://docs.unity3d.com/Manual/StreamingAssets.html

  ​	android平台参考：https://www.cnblogs.com/jpfss/p/9876384.html

- Application.persistentDataPath:(读写) 保存持久数据(对应清空数据)

- Application.temporaryCachePath:(读写)保存少量临时数据(对应清空缓存)

  ​	android平台参考：https://blog.csdn.net/ymlvtimi/article/details/89532191

android平台

| **属性名称**                    | **返回路径**                                                 |
| ------------------------------- | ------------------------------------------------------------ |
| Application.dataPaht            | /data/app/xxx.xxx.xxx.apk                                    |
| Application.streamingAssetsPath | jar:file:///data/app/[xxx.xxx.xxx.apk/!/assets](https://link.jianshu.com/?t=http://xxx.xxx.xxx.apk!/assets) |
| Application.persistentDataPath  | /data/data/xxx.xxx.xxx/files                                 |
| Application.temporaryCachePath  | /data/data/xxx.xxx.xxx/cache                                 |



https://www.jianshu.com/p/bbc2690bce30

https://www.cnblogs.com/chongxin/p/3958625.html

