---
author: supay
layout: post
excerpt_separator: <!-- more -->
comments: true
title: ServiceStack.Text and Windows Phone
dsq_thread_id:
  - 345077375
tags:
  - json
  - servicestack.text
  - windowsphone
  - wp7
post_format: [ ]
---
Recently for one of my projects at work we needed a fast and easy to use JSON Serializer and I immediately remembered a [tweet][1] from [Jeff Atwood][2] with a link to a list of [open source projects][3] that they had at Stack Exchange. Among them they had and amazingly fast JSON serializer [ServiceStack.Text][4].

So, I decided to give it a try. However after I downloaded the project and tried to use it in a sample Windows Phone  project, I found out that ServiceStack.Text was lacking Windows Phone support. However it did support Silverlight 4&5, Xbox and Mono.
<!-- more -->
After a quick search over [DuckDuckGo.com][5] (which by the way has become my main search engine) I found a [blog post][6] by [Chris Santy][7] where he writes about some changes he did to ServiceStack.Text in order to use it on the phone. Unfortunately, although he wrote that he will make a pull request with his changes, he never made one.

So, after adding some of his changes (Thank you  Chris!) and some of mine I got a working version of ServiceStack.Text for  Windows Phone. I immediately made a pull request to the main project and today my request was granted. Over the weekend Demis promised to create a build and get it on Nuget. Which is great News for Windows Phone developers and for me personally since this was my first ever pull-request!

Thank you Demis once again for granting my request! Now I can speak of myself as an officialy OpenSource contributor!

But I have to say that although the current version is much faster that [Json.NET][8], it still loses performance compared to [fastJSON][9] for example. Here are some benchmark results for 10000 iterations using a JSON sample from [GitHubRestTests.cs][10]

![Screenshot1]({{ site.baseurl }}images/posts/JSON_1.jpg) ![Screenshot2]({{ site.baseurl }}images/posts/JSON_2.jpg)


\* *Serialize Standard stands for fastJSON implementation.*

If you are a Windows Phone developer go fork [ServiceStack.Text at GitHub][4] and if you have any comments or question, please leave them in the comments section.

Enjoy!

 [1]: https://twitter.com/#!/codinghorror/status/171015886331846656 "@codinghorror"
 [2]: http://twitter.com/#!/codinghorror "Jeff Atwood"
 [3]: http://blog.stackoverflow.com/2012/02/stack-exchange-open-source-projects/ "Stack Exchange Open Source Projects"
 [4]: https://github.com/ServiceStack/ServiceStack.Text "ServiceStack.Text at GitHub"
 [5]: http://DuckDuckGo.com "DuckDuckGo.com"
 [6]: http://blog.csainty.com/2011/10/using-servicestacktext-for-json.html "Using ServiceStack.Text for JSON processing on Windows Phone 7"
 [7]: https://twitter.com/csainty "Chris Santy"
 [8]: http://json.codeplex.com/ "Json.NET"
 [9]: http://fastjson.codeplex.com/ "fastJSON"
 [10]: https://github.com/ServiceStack/ServiceStack.Text/blob/master/tests/ServiceStack.Text.Tests/UseCases/GitHubRestTests.cs
