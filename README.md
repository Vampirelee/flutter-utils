# flutter-utils
开发flutter中使用的一些坑
## 安卓配置
maven 需要使用国外代理，配置如下, 文件位置：{ProjectRoot}/android/build.gradle，修改成如下
```gradle
allprojects {
    repositories {
        // google()
        // mavenCentral()
        maven {
            allowInsecureProtocol = true
            url 'https://maven.aliyun.com/repository/google'
        }
        maven {
            allowInsecureProtocol = true
            url 'https://maven.aliyun.com/repository/jcenter'
        }
        maven {
            allowInsecureProtocol = true
            url 'http://maven.aliyun.com/nexus/content/groups/public'
        }
        maven { 
            allowInsecureProtocol = true
            url 'https://maven.aliyun.com/repository/gradle-plugin'
        } 
    }
}

rootProject.buildDir = "../build"
subprojects {
    project.buildDir = "${rootProject.buildDir}/${project.name}"
}
subprojects {
    project.evaluationDependsOn(":app")
}

tasks.register("clean", Delete) {
    delete rootProject.buildDir
}

```

flutter SDK配置
文件位置：{flutter SDK}/packages/flutter_tools/gradle/src/main/groovy/flutter.groovy
更改两个地方：

1. buildscript.repositories
     ```groovy
        // google()
        // mavenCentral()
        maven {
            allowInsecureProtocol = true
            url 'https://maven.aliyun.com/repository/google'
        }
        maven {
            allowInsecureProtocol = true
            url 'https://maven.aliyun.com/repository/jcenter'
        }
        maven {
            allowInsecureProtocol = true
            url 'http://maven.aliyun.com/nexus/content/groups/public'
        }
     ```
2. private static final String DEFAULT_MAVEN_HOST = "https://storage.googleapis.com" 修改为
    ```groovy
    private static final String DEFAULT_MAVEN_HOST = "https://storage.flutter-io.cn"
    ```
