# Dubbo 包方法没有参数名

打出来的 dubbo 包在调用的时候看不到方法的参数名

默认情况下，Java编译器会将方法参数的名称替换为 `arg0`、`arg1`、`var1`、`var2` 等，以减少.class文件的大小。

在 `pom.xml` 文件中添加以下配置：

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.8.1</version>
            <configuration>
                <compilerArgs>
                    <arg>-parameters</arg>
                </compilerArgs>
            </configuration>
        </plugin>
    </plugins>
</build>

```
