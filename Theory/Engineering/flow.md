## 前端工程化—流程

### 为什么需要对开发流程进行控制？

如今的前端项目都比较复杂，不同的项目可能使用不同的脚手架，使用不同的构建工具，这些还只是技术上的问题。还要考虑人的因素，多人协同开发会引发的规范、代码风格等问题。所以就需要工程化思想，对项目开发中的各个环节进行流程化控制。

### 如何控制开发流程？应该控制哪些开发流程？
#### 1.统一编码规范，便于团队协作和维护；统一目录结构及文件命名规范。
各个团队成员的编码风格可能会迥然不同，所以需要对一些比较常见的编码规范进行统一，对于项目的目录结构及文件命名进行统一。通过代码规范化，减少团队成员的沟通成本以及新人的适应成本。
一般通过配置统一的eslint规则进行处理，给git commit命令设置git hook，在提交代码之前进行代码规范校验，直到所有代码通过校验才能提交commit。

#### 2.前后端接口规范
现在的Web项目大都是采用前后端分离的形式进行开发，也就是后端提供API服务。但是通常在项目开发阶段，后端的API还未开发完成，为了不阻碍前端的开发，一般前后端会先约定API接口的定义，然后前端mock数据进行开发。
在定义接口的时候要考虑请求参数的形式、返回参数的形式、请求是Post还是Get请求，如果还能提供一个在线mock数据接口给前端测试就更好了。
这时候也需要对前后端的接口进行规范化。

**规范化前端请求的方式：**
例如POST请求需要携带csrf token，参数名为`_csrf_token`，jsonp请求需要传递callback函数名，参数名为`_callback`。
**规范化后端返回数据的方式：**
后端返回数据的整体数据结构统一。例如：

```javascript
{
  data: {},
  success: true 
}
{
  data: {},
  errorMessage: '未登录',
  success: false 
}
```

将前后端接口定义进行规范化后，前端可以使用统一的request库去发送请求，处理后端返回的数据。后端也可以使用统一的库去处理前端传递的参数，返回数据。


#### 3.版本控制及code review
大家在开发中可能会遇到这样的问题：在本地启动了一个mock服务器，前端代码发送请求到本地的测试域名，测试通过后，提交代码发布，忘记将测试域名改回来，很可能就引发严重的线上问题。

此时就需要完善的code review机制。对于每次的应用发布，在发布前需要进行卡点，必须找团队中其他同学进行code review，在review其他同学的代码时，也一定要严格审核，考虑到改动代码如果出现错误是否会产生大面积的影响。还需要建立完善的风险防范机制，在出现问题时，能及时解决。

同时要对应用代码做好管理，新需求创建应用变更，创建新的feature，不同的需求在不同的分支上进行开发。变更代码必须解决与master代码之间的冲突才能上预发环境，对上线之前的流程设置hook，进行**分支检查和版本号检查**。必须验证通过和code review通过才能发布代码。变更代码和master代码的合并通过脚本实现。