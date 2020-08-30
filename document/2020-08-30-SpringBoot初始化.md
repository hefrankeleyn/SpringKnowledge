# SpringBoot初始化

[toc]

## 一、通过`https://start.spring.io/`初始化一个SpringBoot项目

在页面上添加两个依赖：`Spring WEB`、`Actuator`。

## 二、体验其开箱即用的功能

### 2.1 启动应用程序

直接添加`@RestController`和一个`@RequestMapping`启动应用程序。

```java
@SpringBootApplication
@RestController
public class SpringHelloApplication {

	public static void main(String[] args) {
		SpringApplication.run(SpringHelloApplication.class, args);
	}

	@RequestMapping(value = "/hello", method = RequestMethod.GET)
	public String hello(){
		return "hello";
	}
}
```



> curl http://localhost:8080/hello
> hello

> curl http://localhost:8080/actuator/health
> {"status":"UP"}

### 2.2 查看POM文件

这个plugin 会帮助我们在打包的时候，帮我们生成一个可执行的jar包：

```xml
	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
	</build>
```

演示打包：

> mvn clean package -Dmaven.test.skip

### 2.3 通过`java -jar`运行启动应用

> java -jar spring-hello-0.0.1-SNAPSHOT.jar

这样就运行了jar



## 2.4 使用自己的parent，不使用Spring-boot的parent

这个时候pom有两个地方要改变：

```
	<dependencyManagement>
		<dependencies>
			<dependency>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-dependencies</artifactId>
				<version>2.2.5.RELEASE</version>
				<type>pom</type>
				<scope>import</scope>
			</dependency>
		</dependencies>
	</dependencyManagement>
	
		<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
				<executions>
					<execution>
						<goals>
							<goal>repackage</goal>
						</goals>
					</execution>
				</executions>
			</plugin>
		</plugins>
	</build>
```



