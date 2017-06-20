# FE 答疑解惑

包含 HTML, CSS, JavaScript, Node, HTTP 等内容。

## HTML

#### DOCTYPE 作用？有哪些模式？

**答**：DOCTYPE是用来声明文档类型和DTD规范的，一个主要的用途便是文件的合法性验证。 如果文件代码不合法，那么浏览器解析时便会出一些差错。为了能够很好地显示满足标准的页面，又能最大程度兼容不合法的HTML。 浏览器厂商一般会提供两种浏览器模式：

1. 标准模式（standards mode）：浏览器根据标准规约来渲染页面。
2. 混杂模式（quirks mode）：浏览器采用更加宽松的、向后兼容的方式来渲染页面。

混杂模式下，浏览器会模仿旧浏览器的行为，比如IE6，在此基础上兼容新的标准特性。 混杂模式又称兼容模式、怪异模式等。

#### 常用的DOCTYPE声明有几种？

**答**：

1. HTML5 `<!DOCTYPE html>`
2. HTML 4.01 Strict `<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">`
3. HTML 4.01 Transitional

```HTML
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" 
"http://www.w3.org/TR/html4/loose.dtd">
```

#### 什么是 HTML 语义化，为什么要语义化？

**答**：语义化的含义就是用正确的标签做正确的事情，html语义化就是让页面的内容结构化，便于对浏览器、搜索引擎解析。语义化的好处包含

1. 有利于SEO，有助于爬虫抓取更多的有效信息，爬虫是依赖于标签来确定上下文和各个关键字的权重
2. 语义化的HTML在没有CSS的情况下也能呈现较好的内容结构与代码结构
3. 方便其他设备的解析
4. 便于团队开发和维护

#### 行内元素、块级元素、空(void)元素都有那些？

**答**：

* 行内元素：a、b、span、img、input、strong、select、label、em、button、textarea
* 块级元素：div、ul、li、dl、dt、dd、p、h1-h6、blockquote 
* 空元素：即系没有内容的HTML元素，例如：br、meta、hr、link、input、img

#### 简述一下 src 与 href 的区别？

**答**：

* href 是指向网络资源所在位置，建立和当前元素（锚点）或当前文档（链接）之间的链接，用于超链接
* src是指向外部资源的位置，指向的内容将会嵌入到文档中当前标签所在位置；在请求src资源时会将其指向的资源下载并应用到文档内，例如js脚本，img图片和frame等元素。当浏览器解析到该元素时，会暂停其他资源的下载和处理，直到将该资源加载、编译、执行完毕，图片和框架等元素也如此，类似于将所指向资源嵌入当前标签内。这也是为什么将js脚本放在底部而不是头部

#### 请描述一下 HTML 本地化存储都有哪些方案，以及它们之间的区别？

**答**：Cookie, localStorage 和 sessionStorage.

1. Cookie是存储在客户端的小型文本文件，可以包含若干键值对，每个键值对可以设置过期时间（默认过期时间为关闭浏览器时）。 Cookie会在每次发送HTTP请求时附加到Cookie头字段，服务器以此得知用户所处的状态。 在HTTP标准中，规定Cookie至少要有4K，至少支持300项Cookie，每个域名至少支持20项。
2. LocalStorage/SessionStorage提供的存储也是基于字符串的键值对。可以通过setItem，getItem来访问其中的存储项，两者均为 HTML5 标准中新加入的技术，在存储时限上有差别。

以下为三者之间的区别：

<table>
	<thead>
		<tr>
			<th>特性</th>
			<th>Cookie</th>
			<th>localStorage</th>
			<th>sessionStorage</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>数据的生命期</td>
			<td>一般由服务器生成，可设置失效时间。如果在浏览器端生成Cookie，默认是关闭浏览器后失效</td>
			<td>除非被清除，否则永久保存</td>
			<td>仅在当前会话下有效，关闭页面或浏览器后被清除</td>
		</tr>
		<tr>
			<td>存放数据大小</td>
			<td>4K左右</td>
			<td colspan="2">一般为5MB</td>
		</tr>
		<tr>
			<td>与服务器端通信</td>
			<td>每次都会携带在HTTP头中，如果使用cookie保存过多数据会带来性能问题</td>
			<td colspan="2">仅在客户端（即浏览器）中保存，不参与和服务器的通信</td>
		</tr>
		<tr>
			<td>易用性</td>
			<td>需要程序员自己封装，源生的Cookie接口不友好</td>
			<td colspan="2">源生接口可以接受，亦可再次封装来对Object和Array有更好的支持</td>
		</tr>
	</tbody>
</table>

#### 什么是跨域请求？其限制原因有哪些？

**答**：首先需要了解的是同源和跨源的概念。对于相同源，其定义为：如果协议、端口（如果指定了一个）和主机对于两个页面是相同的，则两个页面具有相同的源。只要三者之一任意一点有不同，那么就为不同源。当一个资源从与该资源本身所在的服务器的域或端口不同的域或不同的端口请求一个资源时，资源会发起一个跨域 HTTP 请求。

跨域不一定是浏览器限制了发起跨站请求，而也可能是跨站请求可以正常发起，但是返回结果被浏览器拦截了。

#### 前端跨域请求解决方案都有哪些？

**答**：现主流的解决方案包括： document.domain, location.hash, window.name, window.postMessage, JSONP, WebSocket, CORS 等等。详细描述见 [前端跨域请求解决方案汇总](https://github.com/hijiangtao/hijiangtao.github.io/blob/master/_posts/2017-06-13-Cross-Origin-Resource-Sharing-Solutions.md) 或者 [Joe's Blog](https://hijiangtao.github.io/2017/06/13/Cross-Origin-Resource-Sharing-Solutions/).

#### iframe 的优缺点？

**答**：

优点 

1. 程序调入静态页面比较方便
2. 页面和程序分离
3. 重载页面时不需要重载整个页面，只需要重载页面中的一个框架页(减少了数据的传输，增加了网页下载速度)
4. 能够原封不动的把嵌入的网页展现出来

缺点

1. 会产生很多页面，不容易管理
2. 不容易打印
3. 浏览器的后退按钮无效
4. 代码复杂，无法被一些搜索引擎索引到，这一点很关键，现在的搜索引擎爬虫还不能很好的处理iframe中的内容，所以使用
iframe会不利于搜索引擎优化
5. 多数小型的移动设备无法完全显示框架，设备兼容性差
6. 多框架的页面会增加服务器的http请求，对于大型网站是不可取的

#### iframe 有哪些使用场景？

**答**：

1. 沙箱隔离。
2. 引用第三方内容。
3. 独立的带有交互的内容，比如幻灯片。
4. 需要保持独立焦点和历史管理的子窗口，如复杂的Web应用。

#### HTML 的全局属性都有哪些？

**答**：全局属性是所有HTML元素共有的属性; 它们可以用于所有元素，尽管属性可能对某些元素没有影响。

- `accesskey`:设置快捷键，提供快速访问元素如<a href="#" accesskey="a">aaa</a>在windows下的firefox中按``alt + shift + a``可激活元素
- `class`:为元素设置类标识，多个类名用空格分开，CSS和javascript可通过class属性获取元素
- `contenteditable`: 指定元素内容是否可编辑
- `contextmenu`: 自定义鼠标右键弹出菜单内容
- `data-*`: 为元素增加自定义属性
- `dir`: 设置元素文本方向
- `draggable`: 设置元素是否可拖拽
- `dropzone`: 设置元素拖放类型： copy, move, link
- `hidden`: 表示一个元素是否与文档。样式上会导致元素不显示，但是不能用这个属性实现样式效果
- `id`: 元素id，文档内唯一
- `lang`: 元素内容的的语言
- `spellcheck`: 是否启动拼写和语法检查
- `style`: 行内css样式
- `tabindex`: 设置元素可以获得焦点，通过tab可以导航
- `title`: 元素相关的建议信息
- `translate`: 元素和子孙节点内容是否需要本地化

#### 常见的浏览器内核有哪些？

浏览器内核又可以分成两部分：渲染引擎(layout engineer 或者 Rendering Engine)和 JS 引擎。常见的浏览器内核可以分这四种：Trident、Gecko、Blink、Webkit，此处指浏览器内核。

* Trident 为 IE 内核，又称 MSHTML
* Gecko 内核：Netscape6 开始采用的内核，后来的 Mozilla FireFox(火狐浏览器) 也采用了该内核
* Webkit 内核：Safari, Chrome 等
* Blink 内核：Blink 其实是 WebKit 的分支，如同 WebKit 是 KHTML 的分支
* Presto 内核：Presto 是挪威产浏览器 opera 的 “前任” 内核，最新的 opera 浏览器内核现为 Blink
* 移动端：目前移动设备浏览器上常用的内核有 Webkit，Blink，Trident，Gecko 等，其中 iPhone 和 iPad 等苹果 iOS 平台主要是 WebKit，Android 4.4 之前的 Android 系统浏览器内核是 WebKit，Android4.4 系统浏览器切换到了Chromium，内核是 Webkit 的分支 Blink，Windows Phone 8 系统浏览器内核是 Trident


## JavaScript

## CSS

#### 什么是盒子模型？

**答**：在网页中，一个元素占有空间的大小由几个部分构成，其中包括元素的内容（content），元素的内边距（padding），元素的边框（border），元素的外边距（margin）四个部分。这四个部分占有的空间中，有的部分可以显示相应的内容，而有的部分只用来分隔相邻的区域或区域。4个部分一起构成了css中元素的盒模型。

#### 在一些场景中文本内容不受控制过长超出，有哪些处理超长文本的方法？

**答**：使用 CSS `word-break` 属性（CSS 属性 word-break 指定了怎样在单词内断行的规则）或者 CSS `text-overflow` 属性（text-overflow CSS 属性确定如何向用户发出未显示的溢出内容信号。它可以被剪切，显示一个省略号或显示一个自定义字符串）。

## Node 软件包管理

#### 简述同步和异步之间的区别？

**答**：同步是阻塞模式，异步是非阻塞模式。 同步就是指一个进程在执行某个请求的时候，若该请求需要一段时间才能返回信息，那么这个进程将会一直等待下去，直到收到返回信息才继续执行下去； 异步是指进程不需要一直等下去，而是继续执行下面的操作，不管其他进程的状态。当有消息返回时系统会通知进程进行处理，这样可以提高执行的效率

#### 在每个 package.json 的 dependency 中都会有很多软件名以及随之跟上的版本号，例如 `"d3": "^3.9.0"` 或者 `"d3": "~3.9.0"`，请问 "^" 和 "~" 的含义分别是什么？

**答**：根据 ["npm install --save" No Longer Using Tildes](http://fredkschott.com/post/2014/02/npm-no-longer-defaults-to-tildes/) 一文可知，形如波浪号的编号（例如：~1.2.3）会匹配对应软件所有的 1.2.x 版本，并最终使用最新的符合要求的版本；相比之下倒 V 型编号（例如：^1.2.3）有更松弛的规则，所有 1.x.x 版本均在匹配列表中，但匹配过程会在 2.0.0 停止并返回最新的符合要求的版本。

## HTTP

#### HTTP/0.9 只有一个命令 `GET`, HTTP/1.0 引入了 `POST` 命令和 `HEAD` 命令，丰富了浏览器与服务器的互动手段。请问 HTTP/1.1 的请求方法有哪些？

**答**：HTTP/1.1 提供八种方法以不同的方式操作指定的资源。分别是

1. OPTIONS：这个方法可使服务器传回该资源所支持的所有HTTP请求方法。用'\*'来代替资源名称，向Web服务器发送OPTIONS请求，可以测试服务器功能是否正常运作。
2. HEAD：与GET方法一样，都是向服务器发出指定资源的请求。只不过服务器将不传回资源的本文部分。它的好处在于，使用这个方法可以在不必传输全部内容的情况下，就可以获取其中“关于该资源的信息”（元信息或称元数据）。
3. GET：向指定的资源发出“显示”请求。使用GET方法应该只用在读取数据，而不应当被用于产生“副作用”的操作中，例如在Web Application中。其中一个原因是GET可能会被网络蜘蛛等随意访问。参见安全方法
4. POST：向指定资源提交数据，请求服务器进行处理（例如提交表单或者上传文件）。数据被包含在请求本文中。这个请求可能会创建新的资源或修改现有资源，或二者皆有。
5. PUT：向指定资源位置上传其最新内容。
6. DELETE：请求服务器删除Request-URI所标识的资源。
7. TRACE：回显服务器收到的请求，主要用于测试或诊断。
8. CONNECT：HTTP/1.1协议中预留给能够将连接改为管道方式的代理服务器。通常用于SSL加密服务器的链接（经由非加密的HTTP代理服务器）。

#### HTTP 状态码的主要类型有哪些？

**答**：状态代码的第一个数字代表当前响应的类型，主要为五类

1. 1xx消息——请求已被服务器接收，继续处理
2. 2xx成功——请求已成功被服务器接收、理解、并接受
3. 3xx重定向——需要后续操作才能完成这一请求
4. 4xx请求错误——请求含有词法错误或者无法被执行
5. 5xx服务器错误——服务器在处理某个正确请求时发生错误

详细情况见 [维基百科](https://zh.wikipedia.org/wiki/HTTP%E7%8A%B6%E6%80%81%E7%A0%81)。

#### TCP 协议中为什么连接的时候是三次握手，关闭的时候却是四次握手？

**答**：因为当Server端收到Client端的SYN连接请求报文后，可以直接发送SYN+ACK报文。其中ACK报文是用来应答的，SYN报文是用来同步的。但是关闭连接时，当Server端收到FIN报文时，很可能并不会立即关闭SOCKET，所以只能先回复一个ACK报文，告诉Client端，"你发的FIN报文我收到了"。只有等到我Server端所有的报文都发送完了，我才能发送FIN报文，因此不能一起发送。故需要四步握手。

#### HTTPS 建立连接的过程？

**答**：按照通信过程的收发端来划分，可以将整个过程分成四个部分-客户端请求、服务端回复、客户端回应以及服务器回应。

1. 客户端发出握手请求 (Client Hello)，包含以下信息：
	* 支持的协议版本，比如TLS 1.0
	* 一个客户端生成的随机数(random\_1)，这个随机数既需要客户端保存又需要发送给服务器
	* 支持的加密方法，比如RSA公钥加密
	* 支持的压缩方法
2. 服务器回复 (Server Hello)，包含以下信息：
	* 确认使用的加密通信协议版本，比如TLS 1.0。如果浏览器与服务器支持的版本不一致，服务器关闭加密通信
	* 一个服务器生成的随机数 (random\_2)
	* 确认使用的加密方法，比如RSA公钥加密
	* 服务器证书（其中包含服务器放入公钥）
	* 可选：如果服务器需要确认客户端的身份，就会再包含一项请求，要求客户端提供”客户端证书”。比如，金融机构往往只允许认证客户连入自己的网络，就会向正式客户提供USB密钥，里面就包含了一张客户端证书
3. 客户端回应，包含以下步骤：
	* 验证服务器证书的合法性，证书合法性包括：证书是否过期，发行服务器证书的 CA 是否可靠，发行者证书的公钥能否正确解开服务器证书的“发行者的数字签名”，服务器证书上的域名是否和服务器的实际域名相匹配。如果合法性验证没有通过，通讯将断开
	* 客户端使用一些加密算法 (例如：RSA, Diffie-Hellman)产生一个48个字节的 key，这个 key 叫 PreMaster Secret。该 PreMaster Secret 用服务器发来的公钥加密后随同相关内容（如果前一步，服务器要求客户端证书，客户端会在这一步发送证书及相关信息，即客户的证书以及含有签名的随机数）传送回服务器端，防止被窃听
	* 编码改变通知，表示随后的信息都将用双方商定的加密方法和密钥发送
	* 客户端握手结束通知，表示客户端的握手阶段已经结束。这一项同时也是前面发送的所有内容的hash值，用来供服务器校验
4. 服务器回应，服务器接收到浏览器送过来的消息，用自己的私钥解密，获得 PreMaster Secret。再结合另外两个随机数 random\_1 和 random\_2，计算出本次会话的会话密钥 (session secret)，然后向客户端发送下面信息：
	* 编码改变通知，表示随后的信息都将用双方商定的加密方法和密钥发送
	* 服务器握手结束通知，表示服务器的握手阶段已经结束。这一项同时也是前面发送的所有内容的hash值，用来供客户端校验

在四个过程结束之后，握手阶段结束。接下来，客户端和服务端进入加密通信阶段，该阶段的通信采用普通的 HTTP 协议，只不过双方都采用相同的会话密钥对会话内容进行对称加密和解密。

需要注意的是非对称加解密算法的效率要比对称加解密要低的多。所以 SSL 在握手过程中使用非对称密码算法来协商密钥，实际使用对称加解密的方法对 HTTP 内容加密传输。下图为 SSL 连接建立过程详解图。

![](/assets/img/SSL-Connection-Setup.png "SSL 连接建立过程详解图")

## 参考

* <https://sites.google.com/site/amitsciscozone/home/security/ssl-connection-setup>
* <http://robertheaton.com/2014/03/27/how-does-https-actually-work/>
* <http://www.cnblogs.com/lixiansen/p/5618541.html>
* <http://harttle.com/2016/01/22/doctype.html>
* <http://jerryzou.com/posts/cookie-and-web-storage/>
* <https://www.zhihu.com/question/20653055/answer/17786008>
* <https://developer.mozilla.org/zh-CN/docs/Web/HTML/Global_attributes>
* <http://blog.csdn.net/NJUPT_T/article/details/50700209>
* <http://web.jobbole.com/84826/>

文章参考了以上资源，同时参照 <https://github.com/markyun/My-blog/tree/master/Front-end-Developer-Questions/Questions-and-Answers> 的部分问题列表重新归纳了详细问题答案。