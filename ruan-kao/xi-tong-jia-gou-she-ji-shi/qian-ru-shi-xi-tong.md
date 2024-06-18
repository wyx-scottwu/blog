# 嵌入式系统

### 1. 嵌入式数据库

* 基于内存的数据库MMDB：是实时系统和数据库系统的有机结合。它是支持实时事务的最佳技术，其本质特征是以其“主拷贝”或“工作版本”常驻内存，即活动事务只与实时内存数据库的内存拷贝打交道。&#x20;
* 基于文件的数据库FDB：是以文件方式存储数据数据库数据，即数据按照一定格式存储在磁盘中。使用时由应用程序通过相应的驱动程序甚至直接对数据文件进行读写。这种数据库的访问方式是被动的，只要了解其文件格式，任何程序都可以直接读取，因此它的安全性很低。虽然文件数据库存在诸多弊端，但是，可以满足嵌入式系统在空间、时间等方面的特殊要求。&#x20;
* 基于网络的数据库NDB：是基于手机4G/5G的移动通信基础之上的数据库系统，在逻辑上可以把嵌入式设备看作远程服务器的一个客户端。它无需解析SQL语句；支持更多的SQL操作；客户端小、无须支持可裁剪性；有利于代码重用。

### 2. 嵌入式操作系统

HarmonyOS系统架构整体上遵从分层设计，从下向上分为内核层、系统服务层、框架层和应用层。

HarmonyOS系统功能按照“系统->子系统->功能/模块”逐步逐级展开，在多设备部署场景下，支持根据实际需求裁剪或增加子系统或功能/模块。&#x20;

* 内核层：鸿蒙系统分为内核子系统和驱动子系统。在内核子系统中鸿蒙系统采用多内核设计，支持针对不同资源受限设备选用合适的OS内核；鸿蒙系统驱动框架是鸿蒙系统硬件生态开放的基础，它提供统一外设访问能力和驱动开发、管理框架。
* 系统服务层：系统服务层是鸿蒙系统的核心能力集合，通过框架层对应用程序提供服务。包含了系统基本能力子系统集、基础软件服务子系统集、增强软件服务子系统集、硬件服务子系统四个部分。
* 应用框架层：框架层为鸿蒙系统应用程序提供Java/C/C++/JS等多语言用户程序框架和Ability框架，及各种软硬件服务对外开放的多语言框架API，也为搭载鸿蒙系统的电子设备提供C/C++/JS等多语言框架API。
* 应用层：应用层包括系统应用和第三方非系统应用，鸿蒙系统应用由一个或多个FA或PA组成。

### 3. 总线

<details>

<summary>例题</summary>

以下关于总线的说法中，不正确的是（ ）。

* [ ] A.串行总线适宜于长距离传输数据&#x20;
* [x] B.串行总线传输的波特率是总线初始化时预先定义好的，使用中不可改变&#x20;
* [ ] C.USB接口采用的是串行总线方式&#x20;
* [ ] D.总线上多个设备只能分时向总线发送数据，但可同时从总线接收数据

</details>

关于总线的特点，总结如下：&#x20;

* 串行总线适宜长距离传输数据。 同时串行总线有半双工、全双工之分，全双工是一条线发一条线收。&#x20;
* 串行总线传输的波特率在使用中可以改变。
* 常见串行总线包括： RS232 、SPI、I2C、USB、CAN、IEEE 1394等。&#x20;
* 总线上多个设备只能分时向总线发送数据，但可同时从总线接收数据。

### 4. 混成系统

<details>

<summary>例题</summary>

混成系统是嵌入式实时系统的一种重要的子类。以下关于混成系统的说法中，正确的是（  ）。&#x20;

* [x] A.混成系统一般由离散分离组件并行组成，组件之间的行为由计算模型进行控制
* [ ] B.混成系统一般由离散分离组件和连续组件并行或串行组成 ，组件之间的行为由计算模型进行控制&#x20;
* [ ] C.混成系统一般由连续组件串行组成，组件之间的行为由计算模型进行控制
* [ ] D.混成系统一般由离散分离组件和连续组件并行或串行组成，组件之间的行为由同步/异步事件进行管理&#x20;

</details>

混成系统：一般由离散分离组件和连续组件并行或串行组成，组件之间的行为由计算模型进行控制。