# react 生命周期

![](https://github.com/hevine/react/raw/master/img/001.png)

组件的生命周期分为三个阶段：
Mounted、Updated、Unmounted

* Mounted:当我们能在浏览器中看到组件从无到有的相应效果时，实际 上Mounted 已经结束 了，Mounted结束 ，就说这个组件 被Mounted了

* Updated:而这个重新渲染的过程，并不一定说相应的DOM结构一定会改变，React会把这个Component的当前State和最近一次的State进行对比 ，只有当State确实发生了改变影响到了Dom结构的时候 ，才会去改变对应的Dom结构

* Unmounted 每个状态 React都封装了对应的hook函数 。
   hook函数 最早是指Windows中用于替换Dos下的中断的系统机制，现在是一种泛指，中文翻译 成“钩子”，很传神。
   在对特定的系统 事件hook后，一旦发生已hook事件，则对该事件hook的程序 就会受到系统 的通知。这时程序就会对该事件第一时间作出响应，而对每一种状态react都封装了多个hook函数 

![](https://github.com/hevine/react/raw/master/img/002.png)

 * 在Mounting 这个阶段，可以添加 两个hook函数 分别是 `ComponentWillMount`和`ComponentDidMount` 
 	* `ComponentWillMount`是在component将要被Mounting之前调用
 	* `ComponentDidMount`是在Component被Mounted之后 调用
 * 还有一个用来初始化react Component的state的方法，叫做`getInitialstate()`



 
   `
	var Hello = React.createClass({`	  
	 `  getInitialState:function(){`
	`  	alert('init');`
	`    return {`
	`    	opacity:1.0,`
	 `     fontSize:'12px',`
	  `  } `
	`  },`
	`  render: function() {`
	 ` 	var styleObj = {`
	  `    	color:'red',`
	`      fontSize:'44px'`
	`    }`
	`    return <div style={this.state}>Hello `
	`{this.props.title} {this.props.name}</div>;`
	`  },`
	 ` componentWillMount:function(){`
	 ` 	alert('will');`
	`  },`
	`  componentDidMount:function(){`
	`  	alert('did');`
	`   	var _self = this;`
	 `   window.setTimeout(function(){`
	 `   	_self.setState({`
	  `    	opacity:0.5,`
	 `       fontSize:'44px',`
	 `     });`
	 `   },1000);`
	`  }`
	`});`
	`ReactDOM.render(`
	`  <Hello name="World" title="Mrs"/>,`
	`  document.getElementById('container')`
	`);`
	`doucument.getElementById`
	`('container').style.marginLeft='20px';`
	

#####  怎样修改state?

1. 调用Component的setState方法即可 
2. 将setTimeout中的this取到赋给_self或者使用ES5的bind()方法，略

 发现SetState的值每次变化都会导致component从当前的状态进入到Updating阶段，从而重新render



* 在 Updating这个阶段
	* 首先的两个方法不用说，`ComponentWillUpdate`和`ComponentDidUpdate`这之间就是Render的一个过程
	* 其中一个就是`ComponentWillReceiveProps`，当一个Mounted的Component将要接收一个新的props时，这个函数 会被调用，函数参数就是新的props对象，我们可以在函数体中比较这个函数参数和this.props从而执行一些例如修改state的操作
	* 另一个就是shouldComponentUpdate,当一个Mounted的Component已经接收到新的props和state之后 ，判断 是否有必要修改DOM结构，这个函数 的参数 有两个 新的props对象和新的state对象，分别对比 this.props 和this.state来决定 是否更新DOM结构，此函数 返回true表示 更新，返回false表示 路过这次更新
	 
  这里的几个方法很少用到

* 在Unmounted阶段，只有一个hook函数，`componentWillUnmount`可以执行一些cleanUp的操作，释放内存呀，图片呀什么的，不过得益于浏览器的垃圾回收机制，这个方法也很少去操作。

by hevine 09.12
	 
