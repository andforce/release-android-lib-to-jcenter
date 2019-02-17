# 发布Lib到Jcenter
![](https://img.shields.io/badge/Gradle-v2.14.1-red.svg)
![](https://img.shields.io/badge/Studio-v2.1.3-green.svg)
![](https://img.shields.io/badge/Java-7-blue.svg)

## 准备
+ 注册账号：https://bintray.com (可以用github账号直接授权).
+ 注册完毕之后，记住用户名，其实就是`bintray.apikey`.
+ 在 `Edit Your Profile` -> `API Key` 中获取`bintray.apikey`.

## 如何使用
### 1.使用Android Studio创建 `Android Project`
### 2.在 `local.properties` 在最后添加如下两个属性：
``` script
#注意，等号（=）后不能添加引号（单引号、双引号都不行）
bintray.apikey=YourAPIKey
bintray.user=YourUserName
```
### 3. 修改 `根目录(Project)`build.gradle
+ 添加工具库插件
``` script
buildscript {
    repositories {
        google()
        jcenter()

    }
    dependencies {
        classpath 'com.android.tools.build:gradle:3.3.1'

        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files

        // 添加如下两行
        classpath 'com.jfrog.bintray.gradle:gradle-bintray-plugin:1.8.4'
        classpath 'com.github.dcendents:android-maven-gradle-plugin:2.1'
    }
}
```

### 4.修改`Module的`build.gradle ，在最后添加：
``` script
ext {
    libraryPackaging = 'aar'                                            //上传aar形式的打包文件

    // jcenter
    bintrayRepo = "network"                                             // 你上传的位于bintray中的Repository名称，如果没有创建会有一个叫maven的
    name = 'asyncokhttp'			                                    // 必须和library module的名字相同
    libraryDesc = 'A OkHttp Library'
    publishedGroupId = 'org.zarroboogs.http.asyncokhttp'                // 填写groupId， 一般是包名，比如：com.android.support
    versionName = '1.0.1'			                                    // 版本号，比如：22.2.1
    websiteUrl = 'https://github.com/andforce/AsyncOkHttp'		        // 可以填写github上的库地址.
    issueTrackerUrl = 'https://github.com/andforce/AsyncOkHttp/issues'	// 可以填写github库的issue地址.
    vcsUrl = 'https://github.com/andforce/AsyncOkHttp.git'		        // 可以填写github上库的地址.
    licenseName = "Apache-2.0"
    libraryVersionDesc = 'version descriotion'

    // maven
    artifact = 'asyncokhttp'                                            // 必须和library module的名字相同
    libraryName = 'asyncokhttp'
    developerId = 'anforce'
    developerName = 'andforce'
    developerEmail = '86118@163.com'
    licenseName = 'The Apache Software License, Version 2.0'
    licenseUrl = 'http://www.apache.org/licenses/LICENSE-2.0.txt'
}

apply from: 'https://raw.githubusercontent.com/andforce/release-android-lib-to-jcenter/master/jcenter.gradle'
```

### [](https://github.com/andforce/release-android-lib-to-jcenter#5%E7%BC%96%E8%AF%91%E5%B9%B6%E4%B8%8A%E4%BC%A0%E5%88%B0jcenter)

### 5.编译并上传到Jcenter，在Project根目录执行
``` script
./gradlew jcenter
```
### 6.手动提交到JCenter
执行完上面的步骤，你只是在bintray中创建了一个Package，要发布到JCenter还需要你手动去网站点一下`Add to JCenter`.之后等待审核就好了.

## 完整的使用实例
https://github.com/andforce/AsyncOkHttp

---

## 感谢:
https://github.com/dcendents/android-maven-gradle-plugin
https://github.com/bintray/gradle-bintray-plugin
http://theartofdev.com/2015/02/19/publish-android-library-to-bintray-jcenter-aar-vs-jar-and-optional-dependency/
http://inthecheesefactory.com/blog/how-to-upload-library-to-jcenter-maven-central-as-dependency/en
