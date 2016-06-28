### Subscribe 订阅模式 （观察者模式）

#### 现实中的发布－订阅模式
不管是在现实也好，程序世界也罢，发布订阅模式从来都是于我们形影不离，下面我们举个栗子
老王很想买一张CD,但老板却告知他CD已经卖完了，要等下次进货的时候才会有，于事老王就留了老板号码，每天打一个电话过去问老板CD有没有到货，当然想要CD不只有老王一个， 还有老张，老李等......，他们也跟老王一样， 每天打一个电话过去问老板， 老板烦了， 于是就想到以后有人来问CD就将那人的电话留下，然后告知在CD到货的时候给他们打电话
#### 发布－订阅模式的作用
上面的栗子我们可以看到想买CD的人就相当于程序里的订阅者，老板就相当于程序里的发布者
解决了什么 ？ 
- 老王他们不会每天打电话来问了，顿时心情大好了  
- 发布者与订阅者没有藕合了，以后有想买CD的只要把电话留下，在适当的时间，发布者只要通知这些消息订阅者就好了  
#### DOM事件
实际上，我们经常用到的事件绑定就是发布订阅模式  
```
document.body.addEventListener('click',function(){
  console.log('hello')
},false)
```
在这里我们想在用户点击的时候做出相应的处理，但是我们不知道用户在什么时候去点击，所以我们去订阅body上的click事件，在这里我们还可以去随意增加订阅者，这样并不影响我们的发布者
```
document.body.addEventListener('click',function(){
  console.log('hello2')
},false)
document.body.addEventListener('click',function(){
  console.log('hello3')
},false)
```
#### 自定义事件
除了DOM事件，我们还经常会实现一些自定义事件  
我们一步一步来实现一个自定义事件    
- 谁是发布者  
- 给发布者添加一个缓存列表 
- 发布者遍历缓存列表，依次触发存放的订阅者回调 
```
var cdBoss = {} //cd店老板
cdBoss.clientList = []; // 存放订阅者的回调
cdBoss.listen = function(fn){ // 增加订阅者
  this.clientList.push(fn); // 将订阅者的cb存进缓存列表
}
cdBoss.trigger = function(){ // 发布消息
  for(var i=0,fn; fn= this.clientList[i++];){
    fn.apply(this,arguments) 
  }
}
```
#### 发布－订阅的通用实现
#### 取消订阅的事件
#### 全局的发布－订阅对象
#### 模块间的通信
#### 必须先订阅再发布吗
#### 全局事件的命名冲突
