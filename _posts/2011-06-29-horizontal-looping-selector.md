---
author: supay
layout: post
excerpt_separator: <!-- more -->
comments: true
title: >
  Horizontal Looping Selector for Windows
  Phone
dsq_thread_id:
  - 345077375
tags:
  - code
  - silverlight toolkit
  - wp7
post_format: [ ]
---
The [Silverlight Toolkit for Windows Phone 7][1] contains a lot of really useful controls. One of them is the LoopingSelector which is used by the DatePicker control.

However the limitation of the current Looping Selector is that expands only vertically.But, I needed to do it horizontally.
<!-- more -->
So, I added a few changes to the original LoopingSelector class and created the HorizontalLoopingSelector.

You can compare both looping selectors in the image below.

| HorizontalLoopingSelector | LoopingSelector |
| :------------ | :------------ |
| ![Screenshot1]({{ site.baseurl }}images/posts/screenshot_6-29-2011_14.2.36.9581.png) | ![Screenshot1]({{ site.baseurl }}images/posts/screenshot_6-29-2011_14.19.54.4031.png) |

What I did is add two new files to the *Microsoft.Phone.Controls.Primitives* namespace:

*   HorizontalLoopingSelector.cs
*   HorizontalLoopingSelectorItem.cs

Also, added two new styles for these items to the *Microsoft.Phone.Controls.Toolkit/Themes/Generic.xaml* file. However, these styles do repeat the LoopingSelector and LoopingSelectorItem styles.

I also use a fix for styling the HorizontalLoopigSelector control as [described in Codeplex.com][4]. This allows me use a custom item style for the control as follows:

```xml
<toolkit:HorizontalLoopingSelector Margin="12"
                                   Height="128"
                                   ItemSize="128,128"
                                   ItemTemplate="{StaticResource Temp}"
                                   ItemStyle="MyItemStyle">
```    

You can grab the [sample project][5] from GitHub or download a [package][6] containing only the three modified files.

Hope it will be useful to someone.

 [1]: http://silverlight.codeplex.com/
 [4]: http://silverlight.codeplex.com/workitem/8436 "LoopingSelector Item not style able [WP7 Silverlight Toolkit]"
 [5]: https://github.com/kvervo/HorizontalLoopingSelector/tree/NoDo "GitHub:HorizontalLoopingSelector"
 [6]: https://github.com/downloads/kvervo/HorizontalLoopingSelector/HorizontalLoopingSelector.zip "HorizontalLoopingSelector Package"
