Web（World Wide Web），万维网，汇聚了众多文档资源、多媒体资源的一个庞大网络。网络中有两种节点：Server和Client。资源存储在Server节点，Client节点想要访问Server节点的资源，首先需要知道该资源的URL，再通过HTTP访问。

Client除了可以访问Server的资源，也可以提交信息到Server。Client要提交信息，首先需要明确提交位置（即URL），然后依旧是通过HTTP提交信息。

URL可以标识一个具体的资源，也可以标识一个接口。当标识一个接口时，一般是Client向此接口提交信息。

# Web Server与Web Application Server
Web Server和Web Application Server本质上是运行在Server上的**应用**。

一个应用程序，根据器主要逻辑是运行在Client还是Server，分为非Web应用和Web应用。所有的动态网页几乎都可以被称为Web应用。

在Web中，Server作为物理节点，它主要存储资源，并进行想过逻辑处理。而Web Server作为逻辑节点，在Web中是与其他节点交互的接口，常见的Web Server有：Apache、Nginx。

Web Application Server不仅能够做Web Server所作的事情，还可以处理Web Application的执行。常见的Web Application Server有：TomCat、JBoss、WebLogic。


根据运行平台，应用还可分为：
>桌面应用（Desktop Application）
>移动应用（Mobile Application）
>嵌入式应用（Embedded Application）
>分布式应用（Distributed Application）

# JSP
## 结构
- 客户端发送一个 HTTP 请求给服务器。
    
- Web 服务器识别出这是一个对 JSP 网页的请求，并且将该请求传递给 JSP 引擎。
    
- JSP 引擎从磁盘中载入 JSP 文件，然后将它们转化为 Servlet。这种转化只是简单地将所有模板文本改用 println() 语句，并且将所有的 JSP 元素转化成 Java 代码。
    
- JSP 引擎将 Servlet 编译成可执行类，并且将原始请求传递给 Servlet 引擎。
    
- Web 服务器的某组件将会调用 Servlet 引擎，然后载入并执行 Servlet 类。在执行过程中，Servlet 产生 HTML 格式的输出并将其内嵌于 HTTP response 中上交给 Web 服务器。
    
- Web 服务器以静态 HTML 网页的形式将 HTTP response 返回到客户端。


# Servlet
Servlet是web应用服务器中的一个程序