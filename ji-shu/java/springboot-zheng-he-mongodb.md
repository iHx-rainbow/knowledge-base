# SpringBoot 整合 MongoDB

在Spring Data MongoDB中，可以使用多种方式与MongoDB进行交互，`MongoRepository`是其中最常用的一种，但还有其他方法可以更灵活地操作MongoDB。以下是一些常见的方式：

#### 1. **MongoRepository**

`MongoRepository` 是 Spring Data 提供的一个接口，继承了 `CrudRepository` 和 `PagingAndSortingRepository`，提供了基本的CRUD操作和分页排序功能。只需要定义接口并继承 `MongoRepository`，Spring Data MongoDB 会自动生成相应的实现。

示例：

```java
import org.springframework.data.mongodb.repository.MongoRepository;

public interface UserRepository extends MongoRepository<User, String> {
    List<User> findByLastName(String lastName);
}
```

**优点:**

* 快速简单地实现CRUD操作。
* 支持自动化的查询方法生成。
* 支持分页和排序。

**缺点:**

* 仅适用于基本CRUD操作，复杂查询需要额外处理。

#### 2. **MongoTemplate**

`MongoTemplate` 是 Spring 提供的一个模板类，允许你使用更底层的方式与MongoDB交互。它提供了更大的灵活性，适合处理复杂的查询和更新操作。

示例：

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.data.mongodb.core.MongoTemplate;
import org.springframework.stereotype.Repository;
import com.mongodb.client.result.UpdateResult;

@Repository
public class UserCustomRepository {

    @Autowired
    private MongoTemplate mongoTemplate;

    public User findUserByFirstName(String firstName) {
        Query query = new Query();
        query.addCriteria(Criteria.where("firstName").is(firstName));
        return mongoTemplate.findOne(query, User.class);
    }

    public UpdateResult updateUserLastName(String id, String newLastName) {
        Query query = new Query(Criteria.where("id").is(id));
        Update update = new Update();
        update.set("lastName", newLastName);
        return mongoTemplate.updateFirst(query, update, User.class);
    }
}
```

**优点:**

* 适用于复杂查询和更新操作。
* 提供了更细粒度的控制。

**缺点:**

* 需要手动编写更多代码，相比于 `MongoRepository` 而言，不够简洁。

#### 3. **QueryDSL with MongoDB**

使用 QueryDSL 可以构建类型安全的查询，并与 `MongoRepository` 结合使用。需要配置依赖和生成代码。

示例：

```java
import com.querydsl.core.types.dsl.BooleanExpression;
import org.springframework.data.mongodb.repository.MongoRepository;
import org.springframework.data.querydsl.QuerydslPredicateExecutor;

public interface UserRepository extends MongoRepository<User, String>, QuerydslPredicateExecutor<User> {
}

public class UserService {
    @Autowired
    private UserRepository userRepository;

    public Iterable<User> getUsersByFirstName(String firstName) {
        QUser qUser = QUser.user;
        BooleanExpression predicate = qUser.firstName.eq(firstName);
        return userRepository.findAll(predicate);
    }
}
```

**优点:**

* 提供类型安全的查询。
* 更易于组合和重用查询条件。

**缺点:**

* 需要额外的配置和学习成本。

#### 4. **ReactiveMongoRepository**

适用于构建响应式应用，使用的是Reactive Programming模型。继承自`ReactiveMongoRepository`的接口，提供了响应式的CRUD操作。

示例：

```java
import org.springframework.data.mongodb.repository.ReactiveMongoRepository;
import reactor.core.publisher.Flux;

public interface ReactiveUserRepository extends ReactiveMongoRepository<User, String> {
    Flux<User> findByLastName(String lastName);
}
```

**优点:**

* 适用于响应式编程模型。
* 能更好地处理大规模数据和高并发请求。

**缺点:**

* 需要学习和理解响应式编程模型。

通过这些方式，你可以根据具体需求选择适合的MongoDB交互方式。如果你的应用程序对CRUD操作有更复杂的需求，`MongoTemplate` 和 `QueryDSL` 可能更合适；如果你在构建响应式应用，则`ReactiveMongoRepository`是更好的选择。



{% embed url="https://blog.csdn.net/leesinbad/article/details/128950629" %}
