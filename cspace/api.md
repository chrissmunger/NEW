---
description: 本 Docs会经常更新，可视为 CNS(Coin  Name Service） 白皮书/路线图。
---

# API

REST API、HTTP 请求和响应以及参数的入门读物。​

REST 简介​

了解 HTTP 请求和响应​

提供参数​

数据类型​

如何使用 API 响应数据​

代码中Cspace采用了Cblog举例代替。



## REST 简介​

Cspcae 通过 REST API 提供对其数据的访问。REST 代表 REpresCentational State Transfer，但就我们的目的而言，只需将其视为根据请求发送和接收有关各种资源的信息。 CspcaeREST API 使用 HTTP 处理其请求，使用 JSON 处理其负载。



HTTP 请求和响应​

可以使用某些 HTTP 方法调用 REST API 端点，并且可以在同一个端点上使用多个方法。 Cspcae API 通常会使用以下 HTTP 方法：

GET：读取或查看资源。​

POST：向服务器发送信息。​

PATCH：更新资源。​

DELETE：删除资源。​

你最喜欢的编程语言可能有一个实用程序或库来发出 HTTP 请求。出于本节的目的，将使用 cURL 实用程序作为示例，它是许多操作系统默认包含的命令行实用程序（如<mark style="background-color:blue;">curl</mark>）。

使用 cURL，默认的 HTTP 方法是 GET，但是您可以使用<mark style="background-color:blue;">--requestor-X</mark>标志指定要发出的请求的类型；例如，<mark style="background-color:blue;">curl -X POST</mark>将发送 POST 请求而不是 GET 请求。您可能还希望使用该<mark style="background-color:blue;">-i</mark>标志来包含其他 HTTP 标头，这些标头可能作为相关响应的一部分返回。​

提供参数​

{% hint style="info" %}
API 可以同样理解通过 POST 正文提交的查询字符串、表单数据和 JSON。预计查询字符串用于 GET 请求，而表单数据或 JSON 用于所有其他请求。​
{% endhint %}

查询字符串​

只需请求 URL，但将查询字符串附加到末尾。查询字符串可以通过第一次输入来附加？然后以参数=值的形式附加它们。可以通过用 & 分隔多个查询字符串来附加它们。例如：​

```
//curl https:/CBLOG.me/endpoint?q=test&n=0
```



表单数据​

您可以单独发送数据，而不是使用查询字符串更改 URL。对于 cURL，这是通过使用<mark style="background-color:blue;">--dataor-d</mark>标志传递它来完成的。数据可以像查询字符串一样一起发送，也可以作为具有多个数据标志的键值对单独发送。您还可以将<mark style="background-color:blue;">--formor-F</mark>标志用于键值对，它还允许发送多部分数据，例如文件。例如：​



<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>



JSON​

类似于发送表单数据，但带有一个额外的标头来指定数据为 JSON 格式。要使用 cURL 发送 JSON 请求，请使用标头指定 JSON 内容类型，然后将 JSON 数据作为表单数据发送：​

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>



数据类型​

多个值（数组）​

数组参数必须使用括号表示法编码，例如array\[]=foo\&array\[]=bar将被翻译成以下内容：​

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>



作为 JSON，数组的格式如下：​

嵌套参数（哈希）​

一些参数需要嵌套。为此，还必须使用括号表示法。例如，source\[privacy]=public\&source\[language]=en将被翻译成：​

作为 JSON，哈希的格式如下：​

真或假（布尔值）​

0布尔值对于, f, F, false, FALSE, off,的值被认为是假的，OFF对于空字符串被认为不提供，而对于所有其他值则被认为是真。使用 JSON 数据时，请使用文字true、false和null。​

文件​

文件上传必须使用multipart/form-data​

这也可以与数组结合使用。​



## 如何使用 API 响应数据​

&#x20; Cspcae REST API 将返回 JSON 作为响应文本。它还返回可能对处理响应有用的 HTTP 标头，以及一个 HTTP 状态代码，它应该让您知道服务器如何处理请求。可能会出现以下 HTTP 状态代码：​

200 = 好的。请求已成功处理​

4xx = 客户端错误。您的要求不正确。最常见的是，您可能会看到 401 Unauthorized、404 Not Found、410 Gone 或 422 Unprocessed。​

5xx = 服务器错误。处理请求时出现问题。最常见的是，您可能会看到 503 Unavailable。​
