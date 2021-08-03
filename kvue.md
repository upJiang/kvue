reactive(obj) //接收obj,代理它，实它成为响应式的

副作用函数，当fn中的响应式数据变化时，会主动触发fn的调用，相当于vue3中的watchEffect 跟react中的useEffect

effect(fn) ==> 先调用一次fn() ==> 在调用fn中访问了响应式数据 ==> 于是触发了reactive中的get方法 ==> 那么便触发了依赖收集方法track(target,key)  ==> 建立了 target,key <==> fn 之间的关系 
==> 当响应式数据变化时，就触发了set() ==>trigger()，利用target,key <==> fn 之间的关系再次触发了fn（在例子中update就是fn）

增加虚拟dom,实现h方法,传入（tag, props, children）,在update方法中通过render方法接收，初始化并pathch,新增createElm方法将vnode变成真实dom，通过patch方法对比更新，diff算法

虚拟dom是什么？
虚拟dom就是一个js对象，一个对于真实dom的一个抽象，可以表示一个真实dom的基本结构

为什么需要虚拟dom？
1.虚拟dom可以做到丁点更新，可以对于两次虚拟dom进行对比，只更新变化的节点
2.通过虚拟dom可以更好做跨平台，数据驱动可以直接驱动虚拟dom,渲染层可以更好写出跨平台的代码
3.虚拟dom可以在真实dom生成之前做一些兼容性处理或优化工作，减少人为犯错的可能

vue3编译器优化策略
1.静态节点提升
2.补丁标记和动态属性记录
3.缓存事件处理程序
4.块block
