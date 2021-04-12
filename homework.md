1、请简述 Vue 首次渲染的过程。
答: 在首次渲染之前,先进行 vue 的初始化来初始化实例成员和静态成员,
初始化结束后调用 vue 的构造函数,在构造函数中调用 _init 方法,在 
_init 中调用 $mount 来把模板编译成 render 函数,随后调用 mountComponent
方法,在此方法中先触发 beforeMount 钩子函数,随后创建 Watcher 实例
并调用其 get 方法,在 get 方法中调用 updateComponent 来渲染虚拟 DOM
并将其转换成真实 DOM,然后调用 __patch__ 挂载真实 DOM.

2、请简述 Vue 响应式原理。
答: 在生成vue实例时,为对传入的data进行遍历,使用 Object.defineProperty 
把这些属性转为 getter/setter.每个vue实例都有一个watcher实例,它会在实例
渲染时记录这些属性,并在 setter 触发时重新渲染.vue更新dom时是异步执行的,
数据变化和更新是在主线程中同步执行的,在侦听到数据变化时, watcher 将数据
变更存储到异步队列中,当本次数据变化,即主线程任务执行完毕,异步队列中的任务才会被执行.

3、请简述虚拟 DOM 中 Key 的作用和好处。
答: 作用是便于跟踪每个节点的身份,在进行比较的时候会基于 key 的变化重新排列
元素顺序,从而重用和重新排序现有元素,并且会移除 key 不存在的元素.方便让 vnode
在 diff 的过程中找到对应的节点,然后成功复用.这样可以减少 DOM 操作,减少 diff
和渲染所需要的时间,提升了性能.

4、请简述 Vue 中模板编译的过程。
答: 首先通过 parse 将 template 解析成 AST,其次 optimize 对解析出来的 AST
进行标记,最后 generate 将优化后的 AST 转换成可执行的代码.