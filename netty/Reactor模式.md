Reactor模式的角色构成(Reactor模式一般有五种角色构成):

1. Handle(句柄或是描述符):本质上表是一种资源, 是由操作系统提供的: 该资源用于表示一个个的事件, 比如文件描述符, 或是针对网络编程中的Socket描述符. 事件既可以来自于外部, 也可以来自于内部; 外部事件比如说客户端的连接请求, 客户端发过来的数据等; 内部事件比如说操作系统产生的定时事件等. 它本质上就是一个文件描述符. Handle是事件产生的发源地.

2. Synchronous Event Demultiplexer(同步事件分离器): 它本身是一个系统调用, 用于等待事件的发生(事件可能是一个, 也可能是多个). 调用方在调用它的时候会被阻塞, 同步事件分离器对应的组件就是Selector; 对应的阻塞方法就是select方法

3. Event Handle (事件处理器): 本身由多个回调方法构成,这些回调方法构成了与应用相关的对于某个事件的反馈机制. netty相比与java nio来说, 在事件处理器这个角色上进行了一个升级, 它为我们开发者提供了大量的回调方法, 供我们在特定事件产生时实现相应的回调方法进行业务逻辑处理. 

4. Concrete Event Handle (具体事件处理器); 是事件处理器的实现. 他本身实现了事件处理器所提供的各个回调方法, 从而实现了特定于业务的逻辑. 它本质上就是我们所编写的一个个处理器的实现.

5. Initiaction Dispatcher(初级分发器); 实际上就是Reactor角色. 它本身定义了一些规范, 这些规范用于控制事件的调度方式, 同时又提供了应用进行事件处理器的注册,删除等设施. 它本身是整个事件处理器的核心所在, Initiation Dispatcher会通过同步事件分离器来等待事件的发生. 一旦事件发生, Initation Dispatcher首先会分离出每一个事件, 然后调用事件处理器, 最后调用相关的回调方法来处理这些事件.

----------------------

Reactor模式的流程

1. 当应用向Initation Dispatcher注册具体的事件处理器时, 应用会标识出该事件处理器希望Initiation Dispatcher在某个事件发生时向其通知的该事件, 该事件与Handle关联.

2. Initiation Dispatcher会要求每个事件处理器向其传递内部的Handle. 该Handle向操作系统标识了事件处理器.

3. 当所有的事件处理器注册完毕后, 应用会调用handle_events方法来启动Initiation Dispatcher的事件循环. 这时, Initiation Dispatcher会将每个注册的事件管理器的Handle合并起来, 并使用同步事件分离器等待这些事件的发生. 比如说, TCP协议层会使用select同步事件分离器操作来等待客户端发送的数据到达连接的socket handle上

4. 当与某个事件源对应的Handle变为ready状态时(比如说,TCP socket变为等待读状态时), 同步事件分离器就会通知Initiation Dispatcher

5. Initiation Dispatcher会触发事件处理器的回调方法, 从而响应这个处于ready状态的Handle. 当事件发生时, Initiation Dispatcher会将时间源激活的Handle作为[key]来寻找并分发恰当的事件处理器的回调方法

6. Initiation Dispatcher会回调事件处理器的handle_events回调方法来执行特定于应用的功能(开发者自己所编写的功能), 从而影响这个事件. 所发生的事件类型可以作为该方法参数并被该方法内部使用来执行额外的特定于服务的分离与分发. 