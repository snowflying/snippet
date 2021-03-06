
交换机和路由器
===========

## 交换机的工作原理

From: http://www.cnblogs.com/wuxdotnet/archive/2010/04/07/1706654.html

### 一、交换机的工作原理
    1. 交换机根据收到数据帧中的源MAC地址建立该地址同交换机端口的映射，并将其写入MAC地址表中。
    2. 交换机将数据帧中的目的MAC地址同已建立的MAC地址表进行比较，以决定由哪个端口进行转发。
    3. 如数据帧中的目的MAC地址不在MAC地址表中，则向所有端口转发。这一过程称为泛洪（flood）。
    4. 广播帧和组播帧向所有的端口转发。


### 二、交换机的三个主要功能
以太网交换机了解每一端口相连设备的MAC地址，并将地址同相应的端口映射起来存放在交换机缓存中的MAC地址表中。
　　
#### 转发/过滤
当一个数据帧的目的地址在MAC地址表中有映射时，它被转发到连接目的节点的端口而不是所有端口（如该数据帧为广播/组播帧则转发至所有端口）。

#### 消除回路
当交换机包括一个冗余回路时，以太网交换机通过生成树协议避免回路的产生，同时允许存在后备路径。


### 三、交换机的工作特性
    1. 交换机的每一个端口所连接的网段都是一个独立的冲突域。
    2. 交换机所连接的设备仍然在同一个广播域内，也就是说，交换机不隔绝广播(惟一的例外是在配有VLAN的环境中)。
    3. 交换机依据帧头的信息进行转发，因此说交换机是工作在数据链路层的网络设备(此处所述交换机仅指传统的二层交换设备)。


### 四、交换机的分类
依照交换机处理帧时不同的操作模式，主要可分为两类：

#### 存储转发
交换机在转发之前必须接收整个帧，并进行错误校检，如无错误再将这一帧发往目的地址。帧通过交换机的转发时延随帧长度的不同而变化。

#### 直通式
交换机只要检查到帧头中所包含的目的地址就立即转发该帧，而无需等待帧全部的被接收，也不进行错误校验。由于以太网帧头的长度总是固定的，因此帧通过交换机的转发时延也保持不变。


### 五、`二、三、四层交换机`
多种理解的说法：

##### 二层交换（也称为桥接）是基于硬件的桥接
基于每个末端站点的唯一MAC地址转发数据包。二层交换的高性能可以产生增加各子网主机数量的网络设计。其仍然有桥接所具有的特性和限制。

##### 三层交换是基于硬件的路由选择
路由器和第三层交换机对数据包交换操作的主要区别在于物理上的实施。

##### 四层交换的简单定义
不仅基于MAC（第二层桥接）或源/目的地IP地址（第三层路由选择），同时也基于TCP/UDP应用端口来做出转发决定的能力。其使网络在决定路由时能够区分应用，能够基于具体应用对数据流进行优先级划分。它为基于策略的服务质量技术提供了更加细化的解决方案，提供了一种可以区分应用类型的方法。


## 路由器与交换机的工作原理

From: http://blog.csdn.net/maopig/article/details/6854708

计算机网络往往由许多种不同类型的网络互连连接而成。如果几个计算机网络只是在物理上连接在一起，它们之间并不能进行通信，那么这种“互连”并没有什么实际意义。因此通常在谈到“互连”时，就已经暗示这些相互连接的计算机是可以进行通信的，也就是说，从功能上和逻辑上看，这些计算机网络已经组成了一个大型的计算机网络，或称为互联网络，也可简称为互联网、互连网。

将网络互相连接起来要使用一些中间设备（或中间系统），ISO的术语称之为中继（relay）系统。根据中继系统所在的层次，可以有以下五种中继系统：

    1、物理层（即常说的第一层、层L1）中继系统，即转发器（repeater）。
    2、数据链路层（即第二层，层L2），即网桥或桥接器（bridge）。
    3、网络层（第三层，层L3）中继系统，即路由器（router）。
    4、网桥和路由器的混合物桥路器（brouter）兼有网桥和路由器的功能。
    5、在网络层以上的中继系统，即网关（gateway）。

当中继系统是转发器时，一般不称之为网络互联，因为这仅仅是把一个网络扩大了，而这仍然是一个网络。高层网关由于比较复杂，目前使用得较少。因此一般讨论网络互连时都是指用交换机和路由器进行互联的网络。本文主要阐述交换机和路由器及其区别。

### 交换机和路由器
“`交换`”是今天网络里出现频率最高的一个词，从桥接到路由到ATM直至电话系统，无论何种场合都可将其套用，搞不清到底什么才是真正的交换。其实交换一词最早出现于电话系统，特指实现两个不同电话机之间话音信号的交换，完成该工作的设备就是电话交换机。所以从本意上来讲，**`交换只是一种技术概念，即完成信号由设备入口到出口的转发`**。因此，**`只要是和符合该定义的所有设备都可被称为交换设备`**。由此可见，“交换”是一个涵义广泛的词语，当它被用来描述数据网络第二层的设备时，实际指的是一个桥接设备；而当它被用来描述数据网络第三层的设备时，又指的是一个路由设备。

我们经常说到的以太网交换机实际是一个基于网桥技术的多端口第二层网络设备，它为数据帧从一个端口到另一个任意端口的转发提供了低时延、低开销的通路。

由此可见，_**`交换机内部核心处应该有一个交换矩阵，为任意两端口间的通信提供通路，或是一个快速交换总线，以使由任意端口接收的数据帧从其他端口送出`**_。在实际设备中，**`交换矩阵的功能往往由专门的芯片（ASIC）完成`**。另外，以太网交换机在设计思想上有一个重要的假设，即交换核心的速度非常之快，以致通常的大流量数据不会使其产生拥塞，换句话说，交换的能力相对于所传信息量而无穷大（与此相反，ATM交换机在设计上的思路是，认为交换的能力相对所传信息量而言有限）。

**路由器**是OSI协议模型的网络层中的分组交换设备（或网络层中继设备），**`路由器的基本功能是把数据（IP报文）传送到正确的网络`**，包括：

    1、IP数据报的转发，包括数据报的寻径和传送；
    2、子网隔离，抑制广播风暴；
    3、维护路由表，并与其他路由器交换路由信息，这是IP报文转发的基础。
    4、IP数据报的差错处理及简单的拥塞控制；
    5、实现对IP数据报的过滤和记帐。

**`所谓路由就是指通过相互连接的网络把信息从源地点移动到目标地点的活动`**。一般来说，在路由过程中，信息至少会经过一个或多个中间节点。通常，人们会把路由和交换进行对比，这主要是因为在普通用户看来两者所实现的功能是完全一样的。其实，**`路由和交换之间的主要区别就是交换发生在OSI参考模型的第二层（数据链路层），而路由发生在第三层，即网络层`**。这一区别决定了路由和交换在移动信息的过程中需要使用不同的控制信息，所以两者实现各自功能的方式是不同的。

**交换（switching）**是按照通信两端传输信息的需要，用人工或设备自动完成的方法，把要传输的信息送到符合要求的相应路由上的技术统称。广义的交换机（switch）就是一种在通信系统中完成信息交换功能的设备。

在计算机网络系统中，交换概念的提出是对于共享工作模式的改进。我们以前介绍过的HUB集线器就是一种共享设备，_**HUB本身不能识别目的地址，当同一局域网内的A主机给B主机传输数据时，数据包在以HUB为架构的网络上是以广播方式传输的，由每一台终端通过验证数据包头的地址信息来确定是否接收**_。也就是说，在这种工作方式下，同一时刻网络上只能传输一组数据帧的通讯，如果发生碰撞还得重试。这种方式就是共享网络带宽。

交换机拥有一条很高带宽的背部总线和内部交换矩阵。交换机的所有的端口都挂接在这条背部总线上，控制电路收到数据包以后，处理端口会查找内存中的地址对照表以确定目的MAC（网卡的硬件地址）的NIC（网卡）挂接在哪个端口上，通过内部交换矩阵迅速将数据包传送到目的端口，目的MAC若不存在才广播到所有的端口，接收端口回应后交换机会“学习”新的地址，并把它添加入内部MAC地址表中。

_使用交换机也可以把网络“分段”，通过对照MAC地址表，交换机只允许必要的网络流量通过交换机。通过交换机的过滤和转发，可以有效的隔离广播风暴，减少误包和错包的出现，避免共享冲突。_

交换机在同一时刻可进行多个端口对之间的数据传输。每一端口都可视为独立的网段，连接在其上的网络设备独自享有全部的带宽，无须同其他设备竞争使用。当节点A向节点D发送数据时，节点B可同时向节点C发送数据，而且这两个传输都享有网络的全部带宽，都有着自己的虚拟连接。假使这里使用的是10Mbps的以太网交换机，那么该交换机这时的总流通量就等于2×10Mbps＝20Mbps，而使用10Mbps的共享式HUB时，一个HUB的总流通量也不会超出10Mbps。

总之，_**交换机是一种基于MAC地址识别，能完成封装转发数据包功能的网络设备。交换机可以“学习”MAC地址，并把其存放在内部地址表中，通过在数据帧的始发者和目标接收者之间建立临时的交换路径，使数据帧直接由源地址到达目的地址**_。

### 路由器工作原理
传统地，_路由器工作于OSI七层协议中的第三层，其主要任务是接收来自一个网络接口的数据包，根据其中所含的目的地址，决定转发到下一个目的地址_。因此，**`路由器首先得在转发路由表中查找它的目的地址，若找到了目的地址，就在数据包的帧格前添加下一个MAC地址，同时IP数据包头的TTL（Time To Live）域也开始减数，并重新计算校验和。当数据包被送到输出端口时，它需要按顺序等待，以便被传送到输出链路上`**。

路由器在工作时能够按照某种路由通信协议查找设备中的路由表。如果到某一特定节点有一条以上的路径，则基本预先确定的路由准则是选择最优（或最经济）的传输路径。由于各种网络段和其相互连接情况可能会因环境变化而变化，因此_**路由情况的信息一般也按所使用的路由信息协议的规定而定时更新**_。

网络中，每个路由器的基本功能都是按照一定的规则来动态地更新它所保持的路由表，以便保持路由信息的有效性。为了便于在网络间传送报文，路由器总是先按照预定的规则把较大的数据分解成适当大小的数据包，再将这些数据包分别通过相同或不同路径发送出去。当这些数据包按先后秩序到达目的地后，再把分解的数据包按照一定顺序包装成原有的报文形式。路由器的分层寻址功能是路由器的重要功能之一，该功能可以帮助具有很多节点站的网络来存储寻址信息，同时还能在网络间截获发送到远地网段的报文，起转发作用；选择最合理的路由，引导通信也是路由器基本功能；多协议路由器还可以连接使用不同通信协议的网络段，成为不同通信协议网络段之间的通信平台。

一般来说，路由器的主要工作是对数据包进行存储转发，具体过程如下：

**第一步：**当数据包到达路由器，根据网络物理接口的类型，路由器调用相应的链路层功能模块，以解释处理此数据包的链路层协议报头。这一步处理比较简单，主要是对数据的完整性进行验证，如CRC校验、帧长度检查等。

**第二步：**在链路层完成对数据帧的完整性验证后，路由器开始处理此数据帧的IP层。这一过程是路由器功能的核心。根据数据帧中IP包头的目的IP地址，路由器在路由表中查找下一跳的IP地址；同时，IP数据包头的TTL（Time To Live）域开始减数，并重新计算校验和（Checksum）。

**第三步：**根据路由表中所查到的下一跳IP地址，将IP数据包送往相应的输出链路层，被封装上相应的链路层包头，最后经输出网络物理接口发送出去。

简单地说，_**`路由器的主要工作就是为经过路由器的每个数据包寻找一条最佳传输路径，并将该数据包有效地传送到目的站点。由此可见，选择最佳路径策略或叫选择最佳路由算法是路由器的关键所在`**_。为了完成这项工作，在路由器中保存着各种传输路径的相关数据——路由表（Routing Table），供路由选择时使用。上述过程描述了路由器的主要而且关键的工作过程，但没有说明其它附加性能，例如访问控制、网络地址转换、排队优先级等。

### 交换机如何学习MAC地址
一个交换机刚刚启动，MAC表完全是空的。当有一个二层数据帧到来时（假设从Port 1口进来），交换机会提取出源MAC地址，然后将此MAC地址和Port 1端口的对应关系更新到MAC缓存中，作为以后端口转发的依据。但是交换机的MAC地址缓存有个时间限制（即过期时间），一旦MAC地址和Port的对应关系在缓存中的时间超过了过期时间，则交换机会将其清除。
