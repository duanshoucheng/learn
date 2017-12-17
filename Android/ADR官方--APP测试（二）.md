APP的测试是开发过程的一部分。通过对应用程序进行持续的测试，可以在正式发布之前验证APP的正确性、功能行为和可用性。  
另外，测试可以为你开发提供一下的优势：
- 快速的反馈错误；
- 开发周期的早期故障检测。；
- 安全代码重构,让您优化代码而不用担心回归；
- 稳定的开发速度，帮助最小化技术带来的损失。  
 
理解测试金字塔
![图片来源官网](
http://note.youdao.com/yws/public/resource/7abbd32cddd0fa90ad3a7749766e1236/xmlnote/7D88F983C6284836BE58F6AC22C51163/8164)
虽然测试每个类别的比例可以根据应用程序的不同用例,但一般推荐类别为:70%,20%,10%。
# 编写小测试
当添加或者修改一个APP的功能时，需要一个单元测试来验证。
- Robolectric  
如果APP的测试环境需要单元测试与Android框架进行更广泛的交互,可以使用Robolectric。
- Mock objects  
 所谓的mock就是创建一个类的虚假的对象，在测试环境中，用来替换掉真实的对象，以达到两大目的：验证这个对象的某些方法的调用情况，调用了多少次，参数是什么等等；指定这个对象的某些方法的行为，返回特定的值，或者是执行特定的动作。可以使用mockito达到测试。
- Instrumented unit tests  
 一般比local unit tests慢，当需要评估APP在设备硬件上操作的时候最好使用它来测试。

# 编写中间测试 
如果APP的一些组件依赖于物理硬件，这个测试将会很重要。
# 编写大测试
这需要测试从UI到数据业务逻辑层。AndroidJUnitRunner类还支持以下从Android Testing Support Library(ATSL)工具和框架库
## 1. JUnit4 Rules
## 2. Espresso
## 3. UI Automator
## 4. Android Test Orchestrator
Android Test Orchestrator测试每个UI时都 运行在它自己的Instrumentation的沙箱里。通过减少测试间的共性状态和隔离每一个APP测试的崩溃，来增加测试组件的可靠性。