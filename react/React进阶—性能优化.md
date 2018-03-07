## React性能优化思路

- 软件的性能优化思路就像生活中去看病，大致是这样的：

- 使用工具来分析性能瓶颈（找病根）

- 尝试使用优化技巧解决这些问题（服药）

- 使用工具测试性能是否确实有提升（疗效确认）

## React性能优化的特殊性

看过《高性能JavaScript》这本书的小伙伴都知道，JavaScipt的语言特性、数据结构和算法、浏览器机理、网络传输等都可能导致性能问题。同样是web实现，跟传统的技术（如原生js、jQuery）相比, react的性能优化有什么不同呢？

使用jQuery时，要考虑怎么使用选择器来提高元素查找效率、不要在循环体内进行DOM操作、使用事件委托呀等等。到了React这里，这些东西好像都用不上了。是的，因为React有一个很大的不同点，它实现了虚拟DOM，并且接管了DOM的操作。你不能直接去操作DOM来改变UI，你只能通过改变数据源（props和state）来驱动UI的变化。

说起React的性能分析，还得从它的生命周期和渲染机制说起：

React组件生命周期

![](https://segmentfault.com/img/bVLyCB?w=2803&h=2945)

当 props 和 state 发生变化时，React会根据shouldComponentUpdate方法来决定是否重新渲染整个组件。

### React组件树渲染机制

![](https://segmentfault.com/img/bVLBVL?w=1164&h=742)

父亲组件的props 和 state发生变化时，它和它的子组件、孙子组件等所有后代组件都会重新渲染。

综上所述，可以得出React的性能优化就是围绕shouldComponentUpdate方法（SCU）来进行的，无外乎两点：

- 缩短SCU方法的执行时间(或者不执行)。

- 没必要的渲染，SCU应该返回false。

## React 性能分析工具

#### Web通用工具：Chrome DevTools
最常用到的是Chrome DevTools的Timeline和Profiles。

Timeline工具栏提供了对于在装载你的Web应用的过程中，时间花费情况的概览，这些应用包括处理DOM事件, 页面布局渲染或者向屏幕绘制元素。

通过Timeline发现是脚本问题时，使用Profiles作进一步分析。Profiles可以提供更加详细的脚本信息。

#### React特色工具：Perf
Perf 是react官方提供的性能分析工具。Perf最核心的方法莫过于Perf.printWasted(measurements)了，该方法会列出那些没必要的组件渲染。很大程度上，React的性能优化就是干掉这些无谓的渲染。

有童鞋开发了Chrome扩展程序“React Perf”（戳这里）。相比自己在代码中插入Perf方法进行分析，这个小工具更加灵活方便，墙裂推荐！

