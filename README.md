# j-webp
Java Image I/O reader and writer for the Google WebP image format.

基于[webp project of Luciad](https://bitbucket.org/luciad/webp-imageio) 0.4.2版本修改.

实际上只修改了`com.luciad.imageio.webp.WebP.loadNativeLibrary`这一个方法.  
因为按他默认的加载方式, 需要把native的so/dll/dylib等文件放到OS对应的`java.library.path`对应的目录才能加载到, 这会给部署带来一些不便.

所以我们这里换成了[native-lib-loader](https://github.com/scijava/native-lib-loader)自动加载, 编译构建好的包里已经包含了各种OS上的native文件, 使用时会自动加载.

具体使用方法可参看`src/main/java/example`下的源码.