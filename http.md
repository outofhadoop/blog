[TOC]



# 请求相应的结构

![请求和相应的图片，来自MDN](https://media.prod.mdn.mozit.cloud/attachments/2016/08/31/13827/2737306def7d994b1785d5879f0f5704/HTTPMsgStructure2.png)

1. 一行起始行：用来描述要执行的请求，或对应的状态成功、失败等（起始行总是单行的）。
2. 可选的HTTP头集合（即http headers）：用来指明请求或描述消息正文。
3. 一个空行：指示所有请求元数据已经发送完毕。
4. 可选的包含请求相关数据的正文。



## 起始行

### 1. HTTP方法

* [GET](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/GET)
* [HEAD](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/HEAD)
* [POST](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/POST)
* [PUT](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/PUT)
* [DELETE](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/DELETE)
* [CONNECT](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/CONNECT)
* [OPTIONS](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/OPTIONS)
* [TRACE](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/TRACE)
* [PATCH](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/PATCH)

### 2. 请求目标 (request target)，路径/查询字符串/

详情参考[HTTP请求](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Messages#http_%E8%AF%B7%E6%B1%82)

### 3. HTTP版本 *(HTTP version*)

> 定义了剩余报文的结构，作为对期望的响应版本的指示符。

### 4. Status Code

* [100 Continue](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/100)：表示客户端应继续请求，如果请求完成则忽略。
* [101 Switching Protocol](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/101)：表示服务器回应客户端升级协议的请求，正在切换协议。
* [103 Early Hint](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/103)：允许用户在服务器还在准备响应数据的时候预加载一些资源。
* [200 OK](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/200)：表示请求已经成功；默认情况下状态码为200的响应可以缓存。
* [201 Created](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/201)：表示请求已经成功，并且创建了新的资源；通常应答消息体是新创建的资源。
* [202 Accepted](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/202)：表示服务端已经收到请求消息，但尚未进行处理。
* [203 Non-Authoritative Information](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/203)：表示请求已经被成功响应，但是响应被代理服务器或负载修改过。
* [204 No Content](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/204)：表示响应已经成功，但是客户端不需要离开当前页面。
* [205 Reset Content](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/205)：用来通知客户端重置文档视图。
* [206 Partial Content](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/206)：表示请求成功响应，并且包含所请求的数据区间。
* [300 Multiple Choices](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/300)：表示该请求拥有多种可能的重定向响应。
* [301 Moved Permanently](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/301)：表示请求的资源已经被永久移动到了由[Location](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Location)指定的url上；搜索引擎会根据该项做出修正。
* [302 Found](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/302)：表明请求的资源被暂时移动到了由[Location](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Location)指定的URL上；浏览器会重定向，但搜索引擎不会更新该资源的链接。
* [303 See Other](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/303)：表示重定向链接指向的不是资源，而是另一个页面；**请求重定向后页面的方法总是需要```GET```方法**。
* [304 Not Modified](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/304)：表示无需再次传输请求的内容，可以使用缓存的内容。
* [307 Temporary Redirect](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/307)：表示请求的资源暂时的被移动到了[Location](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Location)所指定的URL地址上；**原始请求中的请求头和方法会被重定向请求重用**；```307```与[302 Found](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/302)的唯一区别在于，发送重定向请求的时候，```307```可以确保请求方法和消息主体不会发生变化。
* [308 Permanent Redirect](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/308)：表示请求的资源已经被永久的移动到了由[Location](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Location)指定的URL上；搜索引擎会更新链接，**原始请求中的请求头和方法会被重定向请求重用**。
* [400 Bad Request](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/400)：表明由于语法无效，服务器无法理解该请求；客户端不应该在未经修改的情况下重复此请求。
* [401 Unauthorized](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/401)：表示缺乏目标资源的身份验证凭证，发送的请求未得到满足；通常会与[WWW-Authenticate](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/401)一起发送，其中包含有如何进行验证的信息。
* [404 Not Found](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/404)：无法找到所请求的资源。
* [405 Method Not Allowed](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/405)：表明服务器禁止使用当前HTTP方法。
* [406 Not Acceptable](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/406)：表明服务器无法提供与[Accept-Charset](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Accept-Charset)以及[Accept-Language](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Accept-Language)消息头指定的值相匹配的响应。
* [407 Proxy Authentication Required](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/407)：缺乏代理服务器所要求的身份验证凭证，该代理服务器位于客户端和所请求的服务器之间。
* [408 Request Timeout](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/408)：服务器将没有使用的连接关闭。
* [409 Conflict](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/409)：表示请求与服务器端目标资源的当前状态相冲突。
* [410 Gone](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/410)：表明目标资源在服务器上**永久性丢失**；若不清楚是否为永久性还是临时性，应该使用[404 Not Found](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/404)。
* [411 Length Required](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/411)：表示由于客户端缺少[Content-Length](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Content-Length)首部字段，服务端残忍的拒绝了客户端的请求。
* [412 Precondition Failed](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/412)：通常由于没有满足请求首部字段（可能是[If-None-Match](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/If-None-Match) 或 [If-Unmodified-Since](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/If-Unmodified-Since)）规定的先决条件，从而拒绝对目标资源的请求。
* [413 Payload Too Large](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/413)：表示请求主体的大小超过了服务器规定的限度，服务器可能会关闭连接以防止客户端继续发送该请求。
* [414 URI Too Long](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/414)：表示客户端请求的URI超过了服务器允许的范围。
* [415 Unsupported Media Type](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/415)：表示服务器不支持其有效荷载的形式。
* [416 Range Not Satisfiable](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/416)：所请求的数据区间不在文件范围内。
* [417 Expectation Failed](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/417)：服务器无法满足请求头[Expect](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Expect)中的要求。
* [418 I'm a teapot](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/418)：服务器拒绝泡咖啡，它只是个茶壶；一个愚人节玩笑😜。
* [422 Unprocessable Entity](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/422)：服务器无法处理请求实体。
* [425 Too Early](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/425)：服务器不愿冒险处理该请求，原因是该请求可能会重放，从而遭到重放攻击。
* [428 Precondition Required](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/428)：表示客户端发送的请求缺失条件首部，服务端要求发送。
* [429 Too Many](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/429)：表示在一定时间内客户端发送了太多请求，超出了”频次限制“。
* [431 Request Header Fields Too Large](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/431)：表示请求中的首部字段的值过大，服务器拒绝接受客户端的请求。
* [451 Unavailable For Legal Reasons](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/451)：表示服务器由于法律原因，无法提供客户端请求的资源。
* [500 Internal Server Error](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/500)：服务器错误。
* [501 Not Implemented](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/501)：该请求方法服务器不支持；客户端无法修复该问题，需要服务端修改。
* [502 Bad Gateway](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/502)：网关或代理服务器从上游服务器收到的响应式无效的。
* [503 Service Unavailable](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/503)：表示服务器尚未处于可接受请求的状态；一般会返回[Retry-After](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Retry-After)首部字段。
* [504 Gateway Timeout](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/504)：表示网关或服务器无法在规定的时间内获得响应。
* [505 HTTP Version Not Support](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/505)：服务器不支持请求所使用的HTTP版本。
* [506 Variant Also Negotiates](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/506)：内部服务器配置错误。
* [507 Insufficient Storage](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/507)：服务器不能存储相关内容，服务器不能存储客户端请求体的数据表达形式。
* [508 Loop Detected](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/508)：服务器中断一个操作，因为在处理 具有“Depth: infinity”的请求时遇到了一个无限循环。
* [510 Not Extended](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/510)：服务器不支持客户端发送请求中的拓展声明。
* [511 Network Authentication Required](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/511)：表示客户端需要通过验证才能使用网络。



## Headers

1. [Accept-CH](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Accept-CH)：由**服务器**设置，以指定客户端在后续请求中应包含有哪些[Client-Hints](https://developer.mozilla.org/en-US/docs/Glossary/Client_hints)提示头
2. [Accept-Charset](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Accept-Charset)：用来告知（服务器）客户端可以处理的字符集类型；这里涉及到两个概念：[内容协商机制](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Content_negotiation) 和 [Quality values质量价值](https://developer.mozilla.org/zh-CN/docs/Glossary/Quality_values)。
3. [Accept-Encoding](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Accept-Encoding)：将客户端可以理解的内容编码方式通知给服务端；服务端会选择一个方式，通过[Content-Encoding](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Content-Encoding)通知给客户端。
4. [Accept-Language](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Accept-Language)：允许客户端声明他可以理解的自然语言，以及优先选择的区域方言；服务器会从诸多备选项中选择一项，并通过[Content-Language](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Content-Language)通知它的选择。
5. [Accept-Patch](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Accept-Patch)：通知浏览器请求的媒体类型可以被服务器理解。
6. [Accept-Post](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept-Post)：通知浏览器请求的媒体类型可以被服务器理解。
7. [Accept-Range](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Accept-Ranges)：服务器定义范围请求的单位。
8. [Accept]()：服务器告知客户端可以处理的内容类型，这种类型用[MIME](https://www.iana.org/assignments/media-types/media-types.xhtml)表示。
9. [Access-Control-Allow-Credentials](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Access-Control-Allow-Credentials)：表示是否可以将请求的响应暴露给页面。（跨域相关）
10. [Access-Control-Allow-Headers](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Access-Control-Allow-Headers)：在[preflight request](https://developer.mozilla.org/zh-CN/docs/Glossary/Preflight_request)（预检请求）中，列出了将会在正式请求[Access-Control-Request-Headers](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Access-Control-Request-Headers)字段中出现的首部信息。
11. [Access-Control-Allow-Methods](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Access-Control-Allow-Methods)：在[preflight request](https://developer.mozilla.org/zh-CN/docs/Glossary/Preflight_request)（预检请求）中，明确了客户端所要访问的资源允许使用的方法或方法列表。
12. [Access-Control-Allow-Origin](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Access-Control-Allow-Origin)：指定了该请求的资源是否被允许与给定的[origin](https://developer.mozilla.org/zh-CN/docs/Glossary/Origin)共享。
13. [Access-Control-Expose-Headers](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Access-Control-Expose-Headers)：指定了哪些首部在响应中可以暴露给外部；若不指定，则只有七种简单首部可以暴露给外部：```Cache-Control``` , ```Content-Language``` , ```Content-Length``` , ```Content-Type``` , ```Expires``` , ```Pragma``` 。
14. [Access-Control-Max-Age](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Access-Control-Max-Age)：表明[preflight request](https://developer.mozilla.org/zh-CN/docs/Glossary/Preflight_request)（预检请求）的返回结果可以被缓存多久。
15. [Access-Control-Request-Headers](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Access-Control-Request-Headers)：出现在[preflight request](https://developer.mozilla.org/zh-CN/docs/Glossary/Preflight_request)（预检请求）中，用于通知服务器在真正的请求中会采用哪些请求头。
16. [Access-Control-Request-Methods](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Access-Control-Request-Method)：出现在preflight request（预检请求）中，用于通知服务器在真正的请求中会采用哪些HTTP方法。
17. [Age](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Age)：消息头里包含对象在缓存代理中存贮多长时间，以秒为单位。
18. [Allow](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Allow)：用于枚举资源所支持的HTTP方法的集合，若服务器返回状态码**[405](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/405) Method Not Allowed**，则该首部字段需要同时返回给客户端，说明资源不接受任何HTTP的方法请求。
19. [Alt-Svc](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Alt-Svc)：全称为Alternative-Service，列出当前站点的备选服务器；这篇解释的文章不错：<https://imququ.com/post/http-alt-svc.html> 。
20. [Authorization](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Authorization)：用于验证用户代理身份的凭证。
21. [Cache-Control](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Cache-Control)：用来设置缓存机制；指令是单向的，这意味着出现在请求中的指令，不一定包含在响应中。
22. [Clear-Site-Data](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Clear-Site-Data)：清除当前网站有关的浏览器数据（```cache```，```cookies```，```storage```，```executionContexts```）。
23. [Connection](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Connection)：当前事务完成后，是否会关闭网络连接，或者是keep-alive。
24. [Content-Disposition](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Content-Disposition)：回复的内容该以何种形式展示。
25. [Content-Encoding](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Content-Encoding)：告知客户端改用何种解码方式获取[Content-Type](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Content-Type)中表示的媒体内容。
26. [Content-Language](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Content-Language)：用来说名访问者希望采用的语言或语言组合，多个语言标签需要用逗号隔开。
27. [Content-Length](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Content-Length)：用来指明发送给接收方的消息主体的大小，用十进制表示的八位元组的数目。
28. [Content-Location](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Content-Location)：指定要返回的数据的地址，主要用来指定要访问的资源经过[内容协商](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Content_negotiation)后的URL。
29. [Content-Range](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Content-Range)：显示一个数据片段在文件中的位置。
30. [Content-Security-Policy-Report-Only](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Content-Security-Policy-Report-Only)：用来监测（但不强制执行）政策的影响来尝试政策。是与[内容安全策略（CSP）](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/CSP)相关。
31. [Content-Security-Policy](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Content-Security-Policy)：控制用户代理能够为指定的页面加载哪些资源。
32. [Content-Type](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Content-Type)：用于指示资源的[MIME](https://www.iana.org/assignments/media-types/media-types.xhtml)类型；告诉客户端实际返回内容的内容类型；可以将[X-Content-Type-Options](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/X-Content-Type-Options)设置为```nosniff``` 来防止浏览器进行MIME查找。
33. [Cookie](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Cookie)：可以参考[HTTP Cookies](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Cookies)。
34. [Cross-Origin-Embedder-Policy](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Cross-Origin-Embedder-Policy)：用来防止文档未明确授予文档权限的任何跨域资源（通过[CORP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cross-Origin_Resource_Policy_(CORP))或[CORS](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/CORS)）。
35. [Cross-Origin-Opener-Policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cross-Origin-Opener-Policy)：确保顶部文档的浏览上下文不被跨域文档获取。
36. [Cross-Origin-Resource-Policy](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Cross-Origin-Resource-Policy)：用来阻止浏览器对指定资源的无源跨域/跨站点请求。
37. [Date](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Date)：报文的创建日期和时间。
38. [Device-Memory](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Device-Memory)：跟[Device Memory API](https://developer.mozilla.org/en-US/docs/Web/API/Device_Memory_API)相关，跟[Client-Hints](https://developer.mozilla.org/en-US/docs/Glossary/Client_hints)请求头的作用类似，用来表示客户端设备内存大小；搭配[Accept-CH](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Accept-CH) 和 [Accept-CH-Lifetime](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Accept-CH-Lifetime)。
39. [Digest](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Digest)：一个摘要。
40. [DownLink](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Downlink)：客户端与服务器连接的近似带宽。
41. [Early-Data](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Early-Data)：由某个中间者设置来表示请求已经在TLS early data 中发送。
42. [ECT](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/ECT)：客户端提示服务器有效的网络连接类型（slow-2g，2g，3g，4g）。
43. [ETag](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/ETag)：资源特定版本的标识符；与[If-Match](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/If-Match)配合使用，可以检测’空中碰撞‘的编辑冲突。
44. [Expect-CT](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Expect-CT)：控制站点报告或者强制执行证书透明度要求。
45. [Expect](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Expect)：包含一个期望的条件，当服务器满足条件的情况下才能处理请求（暂时不知道这个能用来干啥）。
46. [Expires](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Expires)：标识资源是否过期；若在[Cache-Control](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Cache-Control)中设置了 ```max-age ``` 或 ```s-maxage``` ，那么```Expires```会被忽略。
47. [Feature-Policy](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Feature-Policy)：启用或禁用浏览器特性。
48. [Forwarded](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Forwarded)：代理服务器的客户端的信息。
49. [From](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/From)：一个电子邮箱地址，这个地址属于发送请求的代理的实际掌控者的人类用户。
50. [Host](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Host)：指明了请求将要发送到的主机名和端口号。
51. [If-Match](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/If-Match)：一般与[ETag](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/ETag)配合使用，在满足条件的情况下才可以完成请求。
52. [If-Modified-Since](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/If-Modified-Since)：服务器只在所请求的资源在给定日期后被修改过的情况下才会完成请求；只能出现在[HEAD](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/HEAD)或[GET](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/GET)请求中；[If-None-Match](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/If-None-Match)优先级更高。
53. [If-None-Match](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/If-None-Match)：当且仅当服务器上没有任何[ETag](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/ETag)值与这个首部中列出的值相匹配的时候，服务器才会执行请求。
54. [If-Range](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/If-Range)：使得[Range](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Range)在一定条件下起作用；多用于断点续传。
55. [If-Unmodified-Since](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/If-Unmodified-Since)：只有当资源在指定的时间之后未修改的情况下，服务器才会执行请求。
56. [Keep-Alive](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Keep-Alive)：设置超时时长和最大请求数；在HTTP/2中，[Connection](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Connection) 和 Keep-Alive 是被忽略的。
57. [Large-Allocation](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Large-Allocation)：告知浏览器可能会申请大内存，以M为单位；目前仅Firefox实现了该功能。
58. [Last-Modified](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Last-Modified)：源头服务器认定的资源做出修改的日期及时间。
59. [Link](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Link)：序列化HTTP头部链接；与外部资源链接元素[<link>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/link)语义上是相同的。
60. [Location](http://localhost:1024/login?redirect=%2Findex)：需要将页面重定向的地址。
61. [NEL](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/NEL)：配置网络请求的日志；一个实验性的东西[Network Error Logging](https://developer.mozilla.org/en-US/docs/Web/HTTP/Network_Error_Logging)。
62. [Origin](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Origin)：请求来自于哪个站点，包含协议类型、域名或IP地址、端口号（可省略）。
63. [Pramga](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Pragma)：没有固定标准，当值为```no-cache```的时候与[Cache-Control](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Cache-Control)作用相同。
64. [Proxy-Authenticate](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Proxy-Authenticate)：指定代理服务器上的资源访问权限采用什么身份验证方式；与[407](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/407)状态码同时出现。
65. [Proxy-Authorization](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Proxy-Authorization)：用户代理发送给代理服务器的用于身份验证的凭证；通常是服务器返回了[407](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/407)状态码和[Proxy-Authenticate](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Proxy-Authenticate)首部后发送的。
66. [Public-Key-Pins-Report-Only](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Public-Key-Pins-Report-Only)：在公钥固定不匹配时，发送报告到```report-uri```。与[HTTP公钥锁定/HTTP Public Key Pinning(HPKP)](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Public_Key_Pinning)相关。
67. [Public-Key-Pins](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Public-Key-Pins)：Web服务器用来加密的公钥信息，如果锚定的加密串与服务器返回的公钥不匹配，那么浏览器不会展示结果；与[HTTP公钥锁定/HTTP Public Key Pinning(HPKP)](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Public_Key_Pinning)相关。
68. [Range](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Range)：告知服务器返回文件的哪一部分。
69. [Referer](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Referer)：当前请求页面的来源页面的地址。
70. [Referrer-Policy](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Referrer-Policy)：哪些信息会在[Referer](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Referer)中发送。
71. [Retry-After](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Retry-After)：需要等待多长时间之后才能继续发送请求。
72. [RTT](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/RTT)：@TODO
73. [Save-Data](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Save-Data)：客户端对减少数据使用量的偏好。```on```代表启用简化数据的模式，```off```相反。
74. [Sec-Fetch-Dest](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Sec-Fetch-Dest)：标明获取数据的类型；属于[Fetch metadata request header](https://developer.mozilla.org/en-US/docs/Glossary/Fetch_metadata_request_header)。
75. [Sec-Fetch-Mode](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Sec-Fetch-Mode)：标明一个请求的模式；属于[Fetch metadata request header](https://developer.mozilla.org/en-US/docs/Glossary/Fetch_metadata_request_header)。
76. [Sec-Fetch-Site](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Sec-Fetch-Site)：请求的发起者的来源于目标来源的关系；属于[Fetch metadata request header](https://developer.mozilla.org/en-US/docs/Glossary/Fetch_metadata_request_header)。
77. [Sec-Fetch-User](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Sec-Fetch-User)：标明一个导航请求是否由用户触发；```?0```表示由用户触发，```?1```表示由用户以外的原因触发；属于[Fetch metadata request header](https://developer.mozilla.org/en-US/docs/Glossary/Fetch_metadata_request_header)。
78. [Sec-WebSocket-Accept](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Sec-WebSocket-Accept)：服务器发送给客户端，可以接收websocket连接；属于[Fetch metadata request header](https://developer.mozilla.org/en-US/docs/Glossary/Fetch_metadata_request_header)。
79. [Server-Timing](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Server-Timing)：显示一些服务器的参数。
80. [Server](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Server)：处理请求的源头服务器所用到的软件的相关信息。
81. [Set-Cookie](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Set-Cookie)：服务器向客户端发送cookie；[HTTP Cookie](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Cookies)。
82. Set-Cookie2：已废弃，应改用[Set-Cookie](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Set-Cookie)。
83. [Source-Map](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/SourceMap)：一个链接到source map 的链接。
84. [Strict-Transport-Security](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Strict-Transport-Security)：通知浏览器只能用HTTPS访问资源。
85. [TE](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/TE)：指定用户代理希望使用的传输编码类型。
86. [Timing-Allow-Origin](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Timing-Allow-Origin)：指定某个站点可以访问[Resource Timing API](https://developer.mozilla.org/zh-CN/docs/Web/API/Resource_Timing_API)。
87. [TK](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Tk)：对请求的跟踪情况。
88. [Trailer](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Trailer)：在分块消息的尾部添加额外的元信息。
89. [Transfer-Encoding](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Transfer-Encoding)：传递信息给用户所采用的编码类型；仅用于两个节点之间的消息传递，而不是所有请求的资源本身。
90. [Upgrade-Insecure-Request](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Upgrade-Insecure-Requests)：客户端发送给服务器，表示客户端优先选择加密且带有身份验证的响应。
91. [Upgrade](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Upgrade)：
92. [User-Agent](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/User-Agent)：包含用户代理软件的应用类型、操作系统、软件开发商及版本号。
93. [Vary](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Vary)：对于未来的一个请求，应该请求新的回复还是应用缓存。
94. [Via](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Via)：由代理服务器添加，包含域名、端口号、协议类型、版本号、别名。
95. [Viewport-Width](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Viewport-Width)：客户端的视图宽度，单位是px。
96. [Want-Digest](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Want-Digest)：主要出现在request中，发送一个或几个摘要类型供服务端选择。
97. [Warning](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Warning)：包含当前报文可能出现的问题；可能出现多个该首部。
98. [Width](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Width)：
99. [WWW-Authentication](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/WWW-Authenticate)：定义了用何种方式获取对资源的链接； [HTTP 身份验证](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Authentication)。
100. [X-Content-Type-Options](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/X-Content-Type-Options)：服务器用来提示客户端一定要遵循[Content-Type](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Content-Type)中对[MIME](https://www.iana.org/assignments/media-types/media-types.xhtml)的设定。
101. [X-DNS-Prefetch-Control](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/X-DNS-Prefetch-Control)：启用或禁用浏览器的DNS预读取功能。
102. [X-Forwarded-For](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/X-Forwarded-For)：用来记录最初发起请求的客户端的地址。
103. [X-Forwarded-Host](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/X-Forwarded-Host)：记录最初发起请求的客户端的初始域名。
104. [X-Forwarded-Proto](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/X-Forwarded-Proto)：记录最初发起请求的客户端的协议类型。
105. [X-Frame-Options](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/X-Frame-Options)：是否能在 ```frame``` , ```iframe```, ```embed```, ```object``` 中展示内容。
106. [X-XSS-Protection](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/X-XSS-Protection)：IE、Chrome、Safari支持，当检测到XSS攻击时，浏览器将停止加载页面。
