# 测试应用
Android测试比较简单。可以通过集成测试框架来扩展测试能力，例如可以集成 Mockito 在本地单元测试中测试 Android API 调用，以及集成 Espresso 或 UI Automator 在仪器测试中模拟用户交互。您可以利用 Espresso 测试记录器自动生成 Espresso 测试。
## 测试类型和位置
Android Studio有两种测试类型：
- 本地单元测试  
 位于 module-name/src/test/java/。这些测试在计算机的本地 Java 虚拟机 (JVM) 上运行。 当您的测试没有Android框架依赖项或当您可以模拟 Android框架依赖项时，可以利用这些测试来尽量缩短执行时间。可以使用Mockito之类的常见模拟库。
- 仪器测试
 位于 module-name/src/androidTest/java/。这些测试需要在手机或模拟器上运行。

当新建项目或添加应用模块时，AS会创建以上所列的测试源集，并在每个源集中加入一个示例测试文件。名称分别为：ExampleInstrumentedTest、ExampleUnitTest
## 添加一个新测试
要创建一个本地单元测试或仪器测试，您可以按照以下步骤新建针对特定类或方法的测试：
1. 打开包含您想测试的代码的 Java 文件。
2. 点击您想测试的类或方法，然后按 Ctrl+Shift+T (⇧⌘T)。
3. 在出现的菜单中，点击 Create New Test。
4. 在 Create Test 对话框中，编辑任何字段并选择任何要生成的方法，然后点击 OK。
5. 在 Choose Destination Directory 对话框中，点击与您想创建的测试类型对应的源集：androidTest 对应于仪器测试，test 对应于本地单元测试。然后点击OK
> 当然也可以在相应的文件夹下自己添加新的测试类。  

请务必在应用模块的 build.gradle 文件中指定测试库依赖项：
```
dependencies {
    // Required for local unit tests (JUnit 4 framework)
    testCompile 'junit:junit:4.12'

    // Required for instrumented tests
    androidTestCompile 'com.android.support:support-annotations:24.0.0'
    androidTestCompile 'com.android.support.test:runner:0.5'
}
```
## 运行测试
在 Project 窗口中，右键点击测试，然后点击 Run .在代码编辑器中，右键点击测试文件中的某个类或方法，然后点击 **Run**
默认情况下，您的测试运行时使用的是AS默认的运行配置。  
如果您想更改某些运行设置（例如仪器运行器和部署选项），可以在 Run/Debug Configurations 对话框中编辑运行配置（点击 Run > Edit Configurations）。

## 使用命令行测试
可以在命令行使用gradle或者adb来测试
### 1. 使用gradle运行单元测试
下面使用表格总结了怎样使用gradle运行单元测试：

Unit Test Type | 命令 | 测试结果位置
---|--- | ---
本地单元测试 | ./gradlew test | HTML 测试结果文件位于path_to_your_project/module_name/build/reports/tests/。XML测试结果文件位于path_to_your_project/module_name/build/test-results/
仪表测试 | ./gradlew connectedAndroidTest（缩写cAT） | HTML 位置: path_to_your_project/module_name/build/outputs/reports/androidTests/connected/ directory.
XML 位置: path_to_your_project/module_name/build/outputs/androidTest-results/connected/ directory.

在使用gradlew test时出现：
```
* What went wrong:
A problem occurred evaluating root project 'AS3Project'.
> Could not find method google() for arguments [] on repository container of type org.gradle.api.internal.artifacts.dsl.DefaultRepositoryHandler.
```
其他的几种测试：
- ./gradlew mylibrary:connectedAndroidTest //只测试mylibrary module.
- ./gradlew test*VariantName*UnitTest //多种模式的单元测试
- ./gradlew connected*VariantName*AndroidTest //多种模式的仪表测试

### 2. 使用ADB运行测试
使用此种测试比别的方式有更多的选择。To run a test from the command-line, you run adb shell to start a command-line shell on your device or emulator, and then in the shell run the am instrument command. You control am and your tests with command-line flags.首先运行adb shell在手机或模拟器中开启一个命令行的shell，然后在该shell运行am instrument 命令。使用am instrument:
1. 首页运行起来该APP在设备中
2. 在命令行中输入：$adb shell am instrument -w <test_package_name>/<runner_class>
    >test_package_name就是AndroidManifest.xml中的包名，runner_class就是需要使用的测试类。结果命令行中显示。runner_class一般是AndroidJUnitRunner

# 使用Espresso Test Recorder创建UI测试
使用该工具能让你为你的APP不用写任何代码来创建UI测试。
首先需要关闭测试设备上的animations。Espresso有两个关键部分组成：UI交互和View上的断言。UI交互需要人为在设备上操作。而断言则是验证可见元素的存在或内容在屏幕上。举个栗子：某个应用有个button按钮，点击的时候会出现一格note，此时测试的使用，UI交互部分就是点击button，然后断言部分就是验证该button是否存在和是否现在该note。下面的内容是怎样使用Espresso Test Recorder创建这些测试组件，并且怎样在完成一次测试保存这些记录。
## 记录UI交互
按照下面的顺序执行：
1. 点击Run>Record Espresso Test.
2. 选择一个需要部署的设备，如果没有可用创建一个android模拟器，然后点击OK。
3. ETR将会触发项目的编译，在ETR运行交互的时候APP必须已经安装并且启动。

# UI/Application 使用Monkey操作
Monkey是运行在手机后缀模拟器上的一个程序，它可以代替人随机的进行一系列例如点击，手势等一些touch事件的用户操作，也可以使用Monkey在一个随机的可重复的方式压力测试正在开发的应用程序。  
Monkey是一个可以在任何设备或模拟器上进行的一个命令工具，它模拟用户发送一些列随机的事件到系统。Monkey包括很多选择，但是可以概括四个关键分类：
- 基本的配置选项，例如设置事件的数量；
- 操作的限制,例如限制测试到一个包中；
- 事件类型和频率；
- Debugging选择。

基本的语法：
```
$ adb shell monkey [options] <event-count>
```
比如：
```
adb shell monkey -p your.package.name -v 500
```
将会启动APP并且发送500次的随机操作事件。
# monkeyrunner
monkeyrunner(mr)和Monkey测试没有任何关系。mr提供API，为单元测试组件，并且是免费的。可以进行功能测试、回归测试。
需要使用python写测试。暂时忽略