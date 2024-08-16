# @Valid 和 @Validated

在Spring框架中，`@Valid` 和 `@Validated` 都用于进行Bean验证，但它们有一些区别：

1. **注解的来源**:
   * `@Valid` 是 JSR-303（Bean Validation）的标准注解，定义在 `javax.validation` 包中。
   * `@Validated` 是 Spring 框架提供的，定义在 `org.springframework.validation.annotation` 包中。
2. **使用场景**:
   * `@Valid` 通常用于单个对象或集合的验证。当我们在控制器方法中使用`@Valid`注解时，Spring会自动调用验证器来验证请求参数。
   * `@Validated` 可以用在类和方法级别，并支持分组验证。分组验证允许你将验证约束分配到不同的组，并在需要时选择性地应用这些组。
3. **分组验证**:
   * `@Valid` 不支持分组验证。
   *   `@Validated` 支持分组验证。可以在注解中指定验证组，以便在特定情况下应用不同的验证逻辑。例如：

       ```java
       @Validated(OnCreate.class)
       public class MyController {
           // 方法体
       }
       ```
4. **示例**:
   *   使用 `@Valid` 进行验证:

       ```java
       @PostMapping("/users")
       public ResponseEntity<String> createUser(@Valid @RequestBody User user) {
           // 方法体
       }
       ```
   *   使用 `@Validated` 进行分组验证:

       ```java
       @PostMapping("/users")
       public ResponseEntity<String> createUser(@Validated(OnCreate.class) @RequestBody User user) {
           // 方法体
       }
       ```

总的来说，如果你只需要基本的验证功能，`@Valid` 是一个更直接的选择。而如果你需要分组验证或其他高级功能，`@Validated` 会更适合你的需求。
