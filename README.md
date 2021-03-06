# .Net Core vs. Go (modified 2016.07.29)
  
Virtual Machines runs by VMware Workstation 12.1.1 build-3770994 on Windows 10 x64  
  
<b>Host Environment</b>  
>Board: Supermicro MBD-X10DAI-O  
>CPU: Intel Xeon E5-2630 V3 (2.4GHz, 20MB Cache) * 2  
>RAM: Samsung 16GB DDR4-2133 ECC REG * 4  
>RAID: LSI9260-8i (RAID10)  
>HDD: TOSHIBA MD03ACA400V (4TB, 7200RPM, 64M, SATAIII) * 4  
>OS: Microsoft Windows 10 Enterprise x64
  
<b>Guest Environment: .NET Core & Go</b>  
>Processors: 4 (1 processors, 4 cores)  
>Memory: 4GB  
>Hard Disk (SCSI): 64GB  
>Network Adapter: NAT  
>OS: Ubuntu Server 16.04 x64  
>Software: Microsoft .NET Core 1.0.1 (Build cee57bf6c981237d80aa1631cfe83cb9ba329f12)  
>Software: Google Go 1.6.3   
  
<b>Guest Environment: Apach JMeter</b>  
>Processors: 16 (1 processors, 16 cores)  
>Memory: 4GB  
>Hard Disk (SCSI): 64GB  
>Network Adapter: NAT  
>OS: Ubuntu Desktop 14.04.4 x64  
>Software: Oracle Java 2 SDK 8  
>Software: Apache JMeter 3.0  



<b>Apache JMeter Configuration</b>  
><b>Plan</b>  
>  
>&nbsp;- <b>Thread Group</b>  
>&nbsp;&nbsp;&nbsp;Number of Threads (users): 128  
>&nbsp;&nbsp;&nbsp;Ramp-Up Period (in seconds): 0  
>&nbsp;&nbsp;&nbsp;Loop Count: 100  
>  
>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- <b>Loop Controller</b>  
>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Lopp Count: 100  
>  
>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- <b>HTTP Request</b>  
>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Implementation:	HttpClient4
  
  
  
## Common

## Web & Database
<b>Case 01: Output Static JSON</b>  

|               | .NET Core                         | .NET Core       | Go            |
| ------------- | ---------------------------------:| ---------------:| -------------:|
| Web Framework |                      ASP.NET Core |    ASP.NET Core |           gin |
| JSON          | System.Runtime.Serialization.Json | Newtonsoft.Json | encoding/json |
| Throughput    |                             16324 |           18094 |         21203 |
| KB/sec        |                              2833 |            2845 |          2961 |

The default JSON Serializer of ASP.NET Core MVC is Newtonsoft.Json.  
  
<b>Case 02: Output Static JSON and Add 1000 times Random Number into List</b>  

|               | .NET Core                         | Go            | Go             |
| ------------- | ---------------------------------:| -------------:| --------------:|
| Web Framework |                      ASP.NET Core |           gin |            gin |
| JSON          | System.Runtime.Serialization.Json | encoding/json |  encoding/json |
| List          |   System.Collections.Generic.List |         slice | container/list |
| Throughput    |                             16901 |          6252 |          21203 |
| KB/sec        |                              2360 |           873 |           2961 |

  
<b>Case 03: Output HTML by Template</b> 

|               | .NET Core          | Go            | Go                    |
| ------------- | ------------------:| -------------:| ---------------------:|
| Web Framework |       ASP.NET Core |           gin |                   gin |
| Template      |              Razor | html/template | valyala/quicktemplate |
| Throughput    |               1449 |           258 |                  1127 |
| KB/sec        |              77722 |         13836 |                 60402 |

  
# Thanks for all help.
>[WangShen Lu](https://www.facebook.com/tkalu) The difference between Go array and slice  
>[mcliment](https://github.com/mcliment) To make comparison fair by adjusting code and settings for .NET Core Project  
