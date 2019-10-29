# webp-imageio-core
forked from qwong/j-webp
Java Image I/O reader and writer for the Google WebP image format without system lib file.

In source program, coders need to put native lib files like .so/.dll/.dylib into the folder of `java.library.path`.

For easier to use, qwong/j-webp (bases on [webp project of Luciad](https://bitbucket.org/luciad/webp-imageio) 0.4.2) import [native-lib-loader](https://github.com/scijava/native-lib-loader) to load native lib files from project resource folder,   instead of `java.library.path`. (more details to see `com.luciad.imageio.webp.WebP.loadNativeLibrary`)

However, coders pefer using jar package instead of source java code in personal project. So I fork and edit qwong/j-webp to privide a usable jar. It is a fat jar includes dependencies and native lib file (includes windows/linux/mac both 32&64bit).

Update 20181119: sync from [webp project of Luciad](https://bitbucket.org/luciad/webp-imageio) 1.0.0

Update 20191029: [prankstrisse](https://github.com/prankstrisse) provides osx64 dylib file

## Usage

Because it is not in maven repo,  so you have to put the jar file `webp-imageio-core-{version}.jar` into libs folder of your project manually.

[Download jar](https://github.com/nintha/webp-imageio-core/releases)

if you use gradle, you can put it into `src/main/resource/libs`, and edit config file`build.gradle` to add local dependencies

```groovy
dependencies {
    compile fileTree(dir:'src/main/resources/libs',include:['*.jar'])
}
```

if you use maven, you can put it `${project.basedir}/libs`, and edit config file `pom.xml` to add local dependencies

```xml
<dependency>  
    <groupId>com.github.nintha</groupId>  
    <artifactId>webp-imageio-core</artifactId>  
    <version>{versoin}</version>  
    <scope>system</scope>  
    <systemPath>${project.basedir}/libs/webp-imageio-core-{version}.jar</systemPath>  
</dependency>
```

The usage of api, you can see example cases in `src/main/java/example`.



## Compiling the native library

download source code of [webp project of Luciad](https://bitbucket.org/luciad/webp-imageio) , and unzip it.

```shell
wget https://bitbucket.org/luciad/webp-imageio/get/873c5677244b.zip -O luciad-webp-imageio-873c5677244b.zip
unzip luciad-webp-imageio-873c5677244b.zip
```

download source code of [google webp project](https://chromium.googlesource.com/webm/libwebp)

```shell
git clone https://chromium.googlesource.com/webm/libwebp
```

or use the [mirror repo](https://github.com/webmproject/libwebp) 

copy folder libwebp into folder luciad-webp-imageio-873c5677244b, and create a directory called `build` in the  folder luciad-webp-imageio-873c5677244b

folder tree like this:

```
luciad-webp-imageio-873c5677244b/
	|_ build/	<-- just created 
	|_ gradle/
	|_ src/
	|_ libwebp/  <-- copy from project libwebp 
	|_ .hgignore
	|....
	|.... (other files)
```

Install CMake 2.8 or newer. CMake can be downloaded from [www.cmake.org](http://www.cmake.org/) or installed using your systems package manager. if you use Win10 and VS 2019, it need CMake 3.14 or newer.

Open a terminal and navigate to the newly created 'build' directory. 

```
cd ./build
cmake ..
cmake --build .
```

The compiled library can be found under the directory `build/src/main/c`

if you need specific the generator-name, please add `-G <generator-name>` parameter for cmake, like this

```shell
// cmake ..
cmake .. -G "Visual Studio 16 2019"
```



## Compiling the Java library

- Run `mvn install` in the root of the project
- The compiled Java library can be found under the `target`directory



