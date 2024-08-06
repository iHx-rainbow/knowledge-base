# Spring Boot Actuator

**Spring Boot Actuator** 是 Spring Boot 提供的一个子项目，用于帮助开发人员监控和管理 Spring Boot 应用程序。Actuator 提供了一系列的生产环境特性，比如健康检查、应用程序信息、度量指标、日志查看和管理等。

#### 主要功能

1. **健康检查（Health Checks）**:
   * 提供应用程序的健康状况信息，如数据库连接状态、磁盘空间、内存使用情况等。
   * 通过访问 `/actuator/health` 端点来获取健康状况的报告。
2. **度量指标（Metrics）**:
   * 收集并展示应用程序的度量指标，如内存使用、垃圾回收次数、请求处理时间等。
   * 可以通过 `/actuator/metrics` 端点查看各类指标数据。
3. **应用信息（Info）**:
   * 提供应用程序的基本信息，如版本号、Git 提交信息、环境配置等。
   * 通过 `/actuator/info` 端点来获取这些信息。
4. **日志级别管理（Loggers）**:
   * 允许动态查看和修改应用程序的日志级别。
   * 通过 `/actuator/loggers` 端点可以查看和调整日志配置。
5. **Thread Dump**:
   * 提供线程转储，用于诊断应用程序的线程问题。
   * 通过 `/actuator/threaddump` 端点可以查看当前的线程状态。
6. **环境信息（Environment）**:
   * 展示应用程序的当前环境属性，如系统环境变量、配置属性等。
   * 可以通过 `/actuator/env` 端点来访问这些信息。
7. **HTTP 路径映射（Mappings）**:
   * 显示所有的 HTTP 路径映射及其对应的处理方法。
   * 通过 `/actuator/mappings` 端点查看。

#### 安全性

Spring Boot Actuator 提供的这些端点可能包含敏感信息，因此默认情况下是关闭或受限访问的。可以通过配置 Spring Security 对这些端点进行保护，确保只有授权用户可以访问。

#### 配置和扩展

Actuator 是高度可配置的，用户可以启用或禁用特定的端点，也可以自定义新的监控端点来扩展功能。

**总结**: Spring Boot Actuator 是一个功能强大的工具，可以帮助你实时监控和管理 Spring Boot 应用程序的各个方面，对于开发和运维人员来说非常有用。
