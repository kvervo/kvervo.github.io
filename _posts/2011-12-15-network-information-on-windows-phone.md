---
author: supay
layout: post
excerpt_separator: <!-- more -->
comments: true
title: Network Information on Windows Phone
dsq_thread_id:
  - 345077375
tags:
  - Network Information wp7
  - wp7
post_format: [ ]
---
For one of my projects I needed to retrieve the exact connection type used on the device. I needed to know exactly, if the user was using a 3G or 2G cellular connection.

So, after a quick search I found the following link: [Microsoft.Phone.Net.NetworkInformation Namespace][1].

I guess most of you have used the [DeviceNetworkInformation][2] class and especially its [NetworkAvailabilityChanged Event][3], which tells us when a connection has been established or lost. Also, this class allows you to determine if Celular and WiFi data are enabled.

However, I needed more information than this class can provide.
<!-- more -->
Among the listed classes on MSDN, I noticed the [NetworkInterfaceList][5] Class.

![Screenshot1]({{ site.baseurl }}images/posts/Screen-Capture-180x300.jpg)

This class contains an enumerable collection of all currently available network connections on your device.  
Plus it provides the following properties for the connection:

| [InterfaceName][6] | Gets the name of the network interface. |
| [Description][7] | Gets a description of the network interface. |
| [InterfaceType][8] | Gets the type of the network interface. |
| [InterfaceSubtype][9] | Gets additional information about the type of the network interface.|
| [InterfaceState][10] | Gets the connection state of the network interface. |
| [Bandwidth][11] | Gets the speed of the network interface. |
| [Characteristics][12] | Gets the characteristics of the network interface. |

So, you we simply iterate the collection that we get when using NetworkInterfaceList:

```csharp
var allNetworks = (new NetworkInterfaceList()).ToList();
for (var i =0; i < allNetworks.Count; i++)
{
    var network = allNetworks.ElementAt(i);
    ...
}
```

So, now you can easily write a check for specific network types or bandwidth.

Hope this tip will be useful.

If you have any comments or suggestions, feel free to leave them in the comments below.

 [1]: http://msdn.microsoft.com/en-us/library/ff707715(v=VS.92).aspx "Microsoft.Phone.Net.NetworkInformation Namespace"
 [2]: http://msdn.microsoft.com/en-us/library/microsoft.phone.net.networkinformation.devicenetworkinformation(v=VS.92).aspx "DeviceNetworkInformation Class"
 [3]: http://msdn.microsoft.com/en-us/library/microsoft.phone.net.networkinformation.devicenetworkinformation.networkavailabilitychanged(v=VS.92).aspx "NetworkAvailabilityChanged Event"
 [5]: http://msdn.microsoft.com/en-us/library/microsoft.phone.net.networkinformation.networkinterfacelist(v=VS.92).aspx "NetworkInterfaceList"
 [6]: http://msdn.microsoft.com/en-us/library/microsoft.phone.net.networkinformation.networkinterfaceinfo.interfacename%28v=VS.92%29.aspx
 [7]: http://msdn.microsoft.com/en-us/library/microsoft.phone.net.networkinformation.networkinterfaceinfo.description%28v=VS.92%29.aspx
 [8]: http://msdn.microsoft.com/en-us/library/microsoft.phone.net.networkinformation.networkinterfaceinfo.interfacetype%28v=VS.92%29.aspx
 [9]: http://msdn.microsoft.com/en-us/library/microsoft.phone.net.networkinformation.networkinterfaceinfo.interfacesubtype%28v=VS.92%29.aspx
 [10]: http://msdn.microsoft.com/en-us/library/microsoft.phone.net.networkinformation.networkinterfaceinfo.interfacestate%28v=VS.92%29.aspx
 [11]: http://msdn.microsoft.com/en-us/library/microsoft.phone.net.networkinformation.networkinterfaceinfo.bandwidth%28v=VS.92%29.aspx
 [12]: http://msdn.microsoft.com/en-us/library/microsoft.phone.net.networkinformation.networkinterfaceinfo.characteristics%28v=VS.92%29.aspx
