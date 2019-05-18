#### 疑问

其实我一直有个疑问，我们拆分应用，从单体一个进程的单体应用，拆成多个，每个都用http web api的方式提供服务的话，这些web api服务都跑在tomcat、jetty这些
servlet容器里面，但是它们对每个请求，都会创建session，而实际上，这些服务都被做成了无状态的，只要授权通过可以调用（最简单的方式，比如约定好，在http header里面
放一个约定好的token字符串），所以是无状态的，而且这些微服务，也没有任何的页面，就是纯粹的数据服务，你给我数据，我做好逻辑，返回数据给你，仅此而已。

那么因为是部署在tomcat上面，通过http访问，我很想知道，每次调用这个服务提供的web api的时候，tomcat会不会创建session，假设某个服务每天被调用100万次，
那么它会创建100万个根本没必要创建的session对象吗，既占用jvm内存空间，又浪费gc的cpu时间。

tomcat是根据收到的http请求里面的cookie，cookie里面有一个sessionId，一个很长的字符串，来辩识http客户端的，同一个客户端，每次都会带上这个sessionId，
如果没有sessionid，就创建一个新的session对象，然后缓存在jvm中，key就是sessionid，sesionId实际上是一个随机字符串，或者说是uuid，反正全局唯一。

如果是浏览器访问tomcat，是一个人在操作浏览器，浏览器第一次访问的时候，request cookie里面是没有sessionId的，tomcat检测不到就会创建一个新session对象，
然后在response cookie里面把sessionId返回回去，浏览器第2次访问到时候，自然就带上来了，所以tomcat为每个浏览器客户端只会创建一个session，这个倒还好，
数量可控。

但是如果是编程的方式，发起一个http 请求来调用微服务的web api的话，每次http请求调用，都是一个新的唯一的请求，并不会带上所谓的cookie数据，那么我就想知道
tomcat收到web api调用请求后，是不是收到一次请求，就创建一个session（因为它在cookie里面找不到sessonId啊）

第2个疑问，现在写程序，都会用到框架，比如用到springmvc，每次请求先由tomcat处理，再交给框架，最后到自己写的controller，即便tomcat不创建sesson，
框架会不会因为功能实现上的原因，对每个请求，都会创建session，拿java web开发来说，request.getSession方法，万一框架调用了呢？

#### 动机

#### 行动
