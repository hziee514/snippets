# snippets



## maven-publish-aar.gradle

帮助android library开发人员将aar包发布到本地有私有maven仓库

1. 配置POM信息

   ```groovy
   //在模块构建脚本中添加group和version, 对用POM中的groupId和version
   //version后缀为SNAPSHOT时将发布到snapshots仓库
   group = 'cn.fullj.android'
   version = android.defaultConfig.versionName
   ```

2. 引用maven-publish-aar.gradle

   ```groovy
   apply from: 'https://raw.githubusercontent.com/hziee514/snippets/master/maven-publish-aar.gradle'
   ```

3. 配置环境变量

   ```properties
   #在全局gradle.properties文件中配置
   MAVEN_REPO_SNAPSHOTS_URL=<私有snapshots仓库地址>
   MAVEN_REPO_RELEASES_URL=<私有releases仓库地址>
   MAVEN_REPO_USERNAME=<私有仓库账号>
   MAVEN_REPO_PASSWORD=<私有仓库密码>
   ```

4. 发布

   ```bat
   gradlew <projectName>:publish
   ```

5. 完整示例

   ```groovy
   apply plugin: 'com.android.library'
   
   android {
       compileSdkVersion 28
   
       defaultConfig {
           minSdkVersion 14
           targetSdkVersion 28
           versionCode 2
           versionName "1.0.1-SNAPSHOT"
   
           testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"
       }
   
       buildTypes {
           release {
               minifyEnabled false
               proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
           }
       }
   
       compileOptions {
           sourceCompatibility JavaVersion.VERSION_1_8
           targetCompatibility JavaVersion.VERSION_1_8
       }
   }
   
   dependencies {
       implementation fileTree(dir: 'libs', include: ['*.jar'])
       testImplementation 'junit:junit:4.12'
   }
   
   group = 'cn.fullj.android'
   version = android.defaultConfig.versionName
   
   apply from: 'https://raw.githubusercontent.com/hziee514/snippets/master/maven-publish-aar.gradle'
   ```

   