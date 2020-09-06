## 思考与问题

### 1. `Angular` 中引入 `Service` 层概念 (依赖注入)

> 官方：
组件不应该直接获取或保存数据，它们不应该了解是否在展示假数据。 它们应该聚焦于展示数据，而把数据访问的职责委托给某个服务。

- [Angular 中的依赖注入](https://angular.cn/guide/dependency-injection)
- 比较于前端应用中的状态管理，`Vue` 中有 `Vuex` 进行管理，`React` 可以利用 `Redux` 和 `Mobx`
- `Service` 层可以进行全局依赖注入（`@Injectable({ providedIn: 'root' })`）或者为单个`Moudel` (`@Injectable({ providedIn: UserModule })`) 注入
- 不同于 Vue 和 React 中一切皆组件的概念，在 Angular 中更为注重 `Moudel` 形式，`Moudel` 可以包含组件、服务、指定、过滤器等等
- `Service`: 本质是一个类，在服务类中封装的是经常用到的数据和方法。
- 有一些内置的服务，我们可以进行二次封装会用 `$http $log $filter $Timeout 和 $interval`

### 2. `Angular` 中的生命周期

```jsx
ngOnChanges()

ngOnInit()

ngDoCheck()

ngAfterContentInit()

ngAfterContentChecked()

ngAfterViewInit()

ngAfterViewChecked()

ngOnDestroy()
```

[对Angular中的生命周期钩子的理解](https://juejin.im/post/6844903489169031182#comment)

### 3. 管道转换数据

管道是用来对数据进行筛选、过滤、格式化

[官方链接](https://angular.cn/guide/pipes)

```jsx
DatePipe：根据本地环境中的规则格式化日期值。

UpperCasePipe：把文本全部转换成大写。

LowerCasePipe ：把文本全部转换成小写。

CurrencyPipe ：把数字转换成货币字符串，根据本地环境中的规则进行格式化。

DecimalPipe：把数字转换成带小数点的字符串，根据本地环境中的规则进行格式化。

PercentPipe ：把数字转换成百分比字符串，根据本地环境中的规则进行格式化。

# 将返回的生日转化为时间
<p>The hero's birthday is {{ birthday | date }}</p>

# 显示为大写字母
<h2>{{[hero.name](http://hero.name/) | uppercase}} Details</h2>
```

### 4. Observable.subscribe()概念

异步的概念？

与 `Promise` 的区别，对比 `Async await`

### 5. 父子组件传值用

```jsx
1. 属性
	# 发送
	<HeroDetailComponent Hero="123"/>
	# 接收
	@Input() hero: Hero

2. 事件
	# 定义
	<HeroDetailComponent (toFatherEvent)="rcvMsg($event)" Hero="123" />
	# 触发
	@Output() toFatherEvent = new EventEmiiter();
	this.toFatherEvent.emit('123')
```

### 6. 指令

在 `Angular` 中，通过扩展 `HTML` 的属性，比如：

```jsx
1.ng-app 指定应用根元素，至少有一个元素指定了此属性。

2.ng-controller 指定控制器

3.ng-show 控制元素是否显示，true显示、false不显示（通过display：none/block来控制）

4.ng-hide 控制元素是否隐藏，true隐藏、false不隐藏

5.ng-if 控制元素是否“存在”，true存在、false不存在（与ng-show区别：当为false的时候，连同整个DOM节点都不存在）

6.ng-src 增强图片路径

7.ng-href增强地址

8.ng-class 控制类名 (后面可接对象,如ng-class="{done: true}")

9.ng-include 引入模板

10.ng-disabled 表单禁用

11.ng-readonly 表单只读

12.ng-checked 单/复选框表单选中

13.ng-selected 下拉框表单选中
```

`Vue` 和 `Angular` 类似，`React` 是通过 `JSX` 的形式来进行操作

还可以进行自定义指令

```jsx
var App = angular.module('App', []);

// 通过模块实例对象的directive方法可以自定义指令
App.directive('tag', function () {

    // 返回一个对象，这个对象就是自定义指令相关的内容
    return {
        // E element
        // A attribute
        // C class
        // M mark replace 必须为true
        restrict: 'ECMA',
        // template: '<ul><li>首页</li><li>列表</li></ul>',
        templateUrl: './list.html',
        // replace: true
    }

});
```

### 7. 作用域

- 每个 `controller` 下的 `$scope` 产生不同的作用域
- 根作用域：`ng-app` 所在的标签内

### 8. 如何开发

Angular中开发模式：

```jsx
我们是这样写 Angular 应用的：
用 Angular 扩展语法编写 HTML 模板， 
用组件类管理这些模板，
用服务添加应用逻辑， 
用模块打包发布组件与服务。

然后，我们通过引导根模块来启动该应用。
Angular 在浏览器中接管、展现应用的内容，并根据我们提供的操作指令响应用户的交互。
```

在Angular开发时，八大组成部分：

```jsx
1、模块
2、组件
3、模板 自带的html标签+指令、绑定相关的ng的语法
4、元数据 告诉 Angular 如何处理一个类。
5、数据绑定
    {{}} () [] [(ngModel)]
6、指令 
        三大类：组件、结构型、属性型
7、服务
    封装一些数据和方法
8、依赖注入
    就是将依赖的服务、模块注入到指定组件、模块中取使用，提供了一种新的实例化的方式（解耦）
```

## Q&A

### 1.部署 `Firebase` 会出的问题

`Firebase login` 连接失败的问题：

原因应该是开了代理的问题，但不开代理又不能连谷歌，所以把电脑环境和终端环境都设置为全局代理

1. 环境：Mac电脑，使用 `shadowsocksX-NG-R8`，开启全局代理

2. 修改 `.zshrc`

`vi ~/.zshrc` ，端口号是 `shadowsocksX-NG-R8` 中 `HTTP` 代理的端口号

```
export http_proxy = http://127.0.0.1:1087;
export https_proxy = $http_proxy
```

3. 运行

```bash
firebase login --no-localhost
```

## 参考

[Angular 官方文档](https://angular.cn/docs)

[Angular 学习资源清单](https://github.com/wendellhu95/blog/issues/10)

[前端知识点总结——Angular](https://segmentfault.com/a/1190000014175073)
