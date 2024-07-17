---
description: GC 参数
---

# 垃圾收集器选择

不同的垃圾收集器有不同的行为和性能特性。可以通过以下参数选择垃圾收集器：

*   **Serial GC**：适用于单线程环境。

    ```sh
    sh复制代码-XX:+UseSerialGC
    ```
*   **Parallel GC**（默认垃圾收集器）：适用于多线程环境。

    ```sh
    sh复制代码-XX:+UseParallelGC
    ```
*   **G1 GC**：适用于低延迟和高吞吐量的需求。

    ```sh
    sh复制代码-XX:+UseG1GC
    ```
*   **ZGC**：适用于低暂停时间的需求。

    ```sh
    sh复制代码-XX:+UseZGC
    ```
*   **Shenandoah GC**：适用于低暂停时间的需求（OpenJDK 版本）。

    ```sh
    sh复制代码-XX:+UseShenandoahGC
    ```

#### 2. **堆内存大小**

设置堆内存的最小值和最大值，以控制垃圾收集的频率和时机：

*   **最小堆内存大小**：

    ```sh
    sh复制代码-Xms<size>
    ```
*   **最大堆内存大小**：

    ```sh
    sh复制代码-Xmx<size>
    ```

例如：

```sh
sh复制代码-Xms512m -Xmx2g
```

#### 3. **垃圾收集阈值**

通过以下参数设置年轻代和老年代的比例，从而影响垃圾收集的频率：

*   **新生代大小**：

    ```sh
    sh复制代码-Xmn<size>
    ```
*   **Eden 区和 Survivor 区的比例**：

    ```sh
    sh复制代码-XX:SurvivorRatio=<ratio>
    ```
*   **最大老年代空间占用比例**（G1 GC 专用）：

    ```sh
    sh复制代码-XX:MaxGCPauseMillis=<ms>
    ```

#### 4. **GC 日志**

启用 GC 日志以便于调试和优化：

*   **启用 GC 日志**：

    ```sh
    sh复制代码-Xlog:gc*:file=gc.log:time,uptime:filecount=10,filesize=10M
    ```

#### 5. **GC 调优参数**

其他一些常用的调优参数：

*   **控制 Full GC 触发的时机**：

    ```sh
    sh复制代码-XX:InitiatingHeapOccupancyPercent=<percent>
    ```

    用于 G1 GC，设置老年代占用达到多少比例时触发混合 GC（Mixed GC）。
*   **设置 Minor GC 触发阈值**：

    ```sh
    sh复制代码-XX:NewRatio=<ratio>
    ```

    控制新生代和老年代的比例。

#### 6. **高级 GC 配置**

对于特定的垃圾收集器，有一些高级配置参数。例如，G1 GC 的一些常用高级参数：

*   **G1 新生代大小百分比**：

    ```sh
    sh复制代码-XX:G1NewSizePercent=<percent>
    ```
*   **G1 最大新生代大小百分比**：

    ```sh
    sh复制代码-XX:G1MaxNewSizePercent=<percent>
    ```

#### 示例配置

假设我们希望配置 G1 GC，并将老年代的使用阈值设置为 75% 时触发垃圾收集，同时设置堆内存大小为 1G 至 4G，可以使用如下配置：

```sh
sh复制代码-Xms1g -Xmx4g -XX:+UseG1GC -XX:InitiatingHeapOccupancyPercent=75
```

通过这些配置选项，您可以更好地控制垃圾收集器的行为，从而优化应用程序的性能和内存使用。具体的配置需要根据应用程序的实际运行情况进行调整和测试。
