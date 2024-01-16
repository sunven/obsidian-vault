
https://docs.gradle.org/current/userguide/compatibility.html

JVM vs JRE vs JDK
- JVM（Java Virtual Machine）：Java 虚拟机是一个虚拟的计算机，它提供了一个独立于硬件和操作系统的运行平台。所有的 Java 程序最后都会被编译为 JVM 能识别的字节码文件，JVM 再把这些字节码文件翻译（解释或编译）为具体平台上的机器指令执行。因此，JVM 起到了“一次编写，到处运行”的关键作用。
- JRE（Java Runtime Environment）：Java 运行时环境主要包含了 JVM 和 Java 类库。它是 Java 程序运行所需要的环境。JVM 负责运行 Java 程序，Java 类库则提供了 Java 程序运行时需要使用的类和接口。
- JDK（Java Development Kit）：Java 开发工具包是 Java 的完整开发环境，它包含了 JRE 和一些开发工具（如编译器、调试器等）。使用 JDK，开发人员可以编写、编译、调试 Java 程序。
- JDK 包含 JRE，JRE 包含 JVM。
- jdk11开始，已经没有单独的jre了。或者说jdk,jre统一了

JavaSE vs JavaEE vs JavaME
- JavaSE（Java Standard Edition）：基础的 Java 版本，提供了标准的 Java 应用程序接口（API）。它包含所有基本的 Java 库和工具，如基本数据类型、IO 流、网络编程、集成库等。JavaSE 主要用于桌面应用程序和服务器端开发。
- JavaEE（Java Enterprise Edition）：是构建企业级应用程序的 Java 平台，基于 JavaSE，包含更多扩展和补充，特别适用于网络应用程序。例如：servlet，JSP，EJB，JMS，Web Service，XML 处理等。另外，JavaEE 支持分布式计算和事务处理，可以处理大数据量，高并发，高可靠性的复杂系统的需求。
- JavaME（Java Micro Edition）：是专为嵌入式系统和小型设备设计的 Java 平台。它针对资源受限的应用提供了一套轻量级的 API，如手机、PDA、TV set-top boxes，工业控制等。
