---
author: supay
layout: post
excerpt_separator: <!-- more -->
comments: true
title: "Smooth Streaming Multi Resolution Support for Windows 
Phone"
date: 2013-01-04 23:17
categories: 
dsq_thread_id:
  - 345077375
tags:
  - ssme
  - smooth streaming
  - windows phone
---

*Disclaimer: The following article does only apply for Windows Phone 7.1 devices. Windows Phone 8 should have no constraints regarding playing multi-resolution streams.*

I believe everyone who tried to create a video streaming app for Windows Phone, found rather frustrating that the Smooth Streaming Media Element did not support multiple resolutions. If you were using a manifest with variable resolutions on your desktop application, you could certainly be sure that this manifest will not work on your Windows Phone app out of the box. You had to handle the [ManifestReady](http://msdn.microsoft.com/en-us/library/microsoft.web.media.smoothstreaming.smoothstreamingmediaelement.manifestready.aspx) event and then use the [RestrickTracks](http://msdn.microsoft.com/en-us/library/microsoft.web.media.smoothstreaming.streaminfo.restricttracks.aspx) method to play only the tracks that had the same resolution. 

However, I never really understood why the Multi-Resolution support was not provided in the Smooth Streaming Media Element Client for Windows Phone.

<!-- more -->

Well, not until I recently read the [Video playback guidance for Nokia Lumia 610](https://www.developer.nokia.com/Community/Wiki/Video_playback_guidance_for_Nokia_Lumia_610) on the [Nokia Developer wiki](http://www.developer.nokia.com/Develop/Windows_Phone/).
<!-- (Which is by the way much better that MSDN or any other Microsoft Documentation website). -->

The reason why first generation devices could not stream multi-resolution video was the processor.   
So, basically Multiple Resolution support is available on Qualcomm 8x55 processors or higher; 7x27a and 8x50 do not support it.

There is even a property that was added to the SDK since version 7.1: [MediaCapabilities.IsMultiResolutionVideoSupported](http://msdn.microsoft.com/en-us/library/microsoft.phone.info.mediacapabilities.ismultiresolutionvideosupported.aspx) which indicates whether the current device supports multi-resolution video.

Also, in [MSDN](http://msdn.microsoft.com/en-us/library/ff462087.aspx) you can find all the information regarding supported media codecs by each processors with specifications about Smooth Streaming support. 

I just do not know, how could I miss it!

Below you will find a table specifically for Smooth Streaming Video Support according to different processors. Notice that I personally work with h.264, therefore the table references only h.264 codec.

| Codec and Profile | Phone chipset | Level | Max average bitrate | Max peak bitrate | Max resolution and framerate |
| :----- | :----- | :----- | :----- | :----- | :----- |
| H.264 Baseline	| 7x27a/baseline | 2.0 | 2 Mbps | 4 Mbps | 800×480 @ 30 fps |
| | 8x50 / 8x55 | 3.1 | 10 Mbps |	 27 Mbps | 1280x720 @ 30 fps |
| H.264 Main 	| 7x27a/baseline | 1.3 - CABAC, 2.0 - CAVL | CABAC: 2 Mbps, CAVLC: 768 Kbps | 4 Mbps | 800×480 @ 30 fps | 
| | 8x50 / 8x55 | 3.1 | 10 Mbps | 27 Mbps | 1280x720 @ 30 fps |
| H.264 High | 7x27a/baseline | 1.3 - CABAC, 2.0 - CAVLC | CABAC: 2 Mbps, CAVLC: 768 Kbps | 4 Mbps | 800×480 @ 30 fps | 
| | 8x50 / 8x55 | 3.1 | 10 Mbps |	27 Mbps | 1280x720 @ 30 fps |

Also, I did a small research of all available devices on the market to find out whether they support multi-resolution smooth streaming video or not.

| OS | Model | CPU | Multi-Res Support |
| :----- | :----- | :----- | :----- |
| WP8 | HTC Windows Phone 8S | MSM8627 | ? |
| 	| HTC Windows Phone 8X | MSM8960 | Yes |
| 	| Nokia Lumia 620*	| MSM8227 ? MSM8627 | ? |
| 	| Nokia Lumia 810	| MSM8960 | Yes |
| 	| Nokia Lumia 820	| MSM8960 | Yes |
|  	| Nokia Lumia 822	| MSM8960 | Yes |
| 	| Nokia Lumia 920	| MSM8960 | Yes |
| 	| Samsung Ativ S	| MSM8960 | Yes |
| WP7.5 | Acer Allegro	| MSM8255 | Yes |
|	| Fujitsu Toshiba IS12T | MSM8655 | Yes |
|	| HTC Radar 4G | MSM8255 | Yes |
|	| HTC Titan (Ultimate/Eternity) | MSM8255T | Yes |
|	| HTC Titan II | MSM8255T / MDM9200 | Yes / ? |
|	| Nokia Lumia 510 | MSM7227A | No |
|	| Nokia Lumia 610 | MSM7227A | No |
|	| Nokia Lumia 710 | MSM8255	| Yes |
|	| Nokia Lumia 800 | MSM8255T | Yes |
|	| Nokia Lumia 900 | APQ8055 | Yes |
|	| Samsung Focus 2* | APQ8055 ? MSM8255 ? MSM8655 | Yes |
|	| Samsung Focus S | MSM8255 | Yes |
|	| Samsung Omnia M | MSM7227A | No |
|	| Samsung Omnia W (Focus Flash) | MSM8255 | Yes |
|	| ZTE Orbit (Render) | MSM7227A | No |
|	| ZTE Tania (Spirit) | MSM8255 | Yes|
|	| Alcatel One Touch View | MSM7227A | No |
| WP7 | Dell Venue Pro | QSD8250 | No |
|	| HTC 7 Pro (Arrive) | QSD8250 / QSD8650 | No / No |
|	| HTC 7 Surround | QSD8250	| No |
|	| HTC 7 Trophy | QSD8250 / QSD8650 | No / No |
|	| HTC 7 Mozart | QSD8250 | No |
|	| HTC HD2 | QSD8250 | No |
|	| HTC HD7 (HD7S) | QSD8650 | No |
|	| LG Optimus 7 (Jil Sander Mobile) | QSD8650 | No|
|	| LG Quantum (Optimus 7Q) | QSD8250 | No |
|	| Samsung Focus | QSD8250 | No |
|	| Samsung Omnia 7 | QSD8250 | No |

\**Information is not complete or no official data was found.*

So, what can you do to start supporting multi-resolution? Well there are a couple of possible solutions:
	
* You could create different manifests files containing only the required resolutions for different kind of devices. Which you could request from the server by passing a custom parameter.
* Also, you could add a **CustomAttribute** tag to each stream and perform the selection based on it's value when handling ManifestReady event. For example:

```xml
<QualityLevel Index="5" Bitrate="307200" FourCC="WVC1" MaxWidth="720" MaxHeight="480" CodecPrivateData = "1207F840">  
    <CustomAttributes>  
        <Attribute Name = "hardwareProfile" Value = "0" />  
    </CustomAttributes>  
</QualityLevel>  
```

* Adding a custom attribute requires you to mess up with the manifest. If you cannot or do not want to do this, you can manually parse the **CodecPrivateData** attribute for each track and based on the retrieved information select different tracks for different devices.

Personally I prefer the last option: parse the CodecPrivateData attribute.

The CodecPrivateData attribute is a base 16 text string and it contains information about h264 profile and level, height and width plus a bunch of different other encoding params.

CodecPrivateData has the following structure:   
0x00000001 **SequenceParameterSet** 0x00000001 **PictureParameterSet**

Please, see [ISO/IEC-14496-10](http://standards.iso.org/ittf/PubliclyAvailableStandards/index.html) for further details on Start Codes (0x00000001), Sequence Parameter Set (SPS) and Picture Parameter Set (PPS) formats.

So, basically you will need to know the following information for a safe choice of tracks:

* Is Multi-Resolution Video Supported
* H.264 Profile
* H.264 Level
* Height
* Width
* Was CABAC used or not
* Was CAVLC used or not

By combining all these params you will be able to filter specific tracks based on supported media codecs information for each type of device.

In the end, I believe this to be the most universal solution. Since you do not need to mess up with the manifest structure in any way. You also do not need to set up proxies to different manifest files. Which is great, specially if you are using 3rd party streaming services that cannot be modified in any way. 

I strongly recommend to take into account this information for your next application update and add Multi-Resolution support to your app.
This way, you could get rid of reviews like '**bad video quality**' once and for all. However, you may start getting more hateful reviews like '**battery drainer**', be ready :)
