# 🚀 高并发秒杀系统

[![Java](https://img.shields.io/badge/Java-1.8+-orange.svg)](https://www.oracle.com/java/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-2.6.5-brightgreen.svg)](https://spring.io/projects/spring-boot)
[![Redis](https://img.shields.io/badge/Redis-6.0+-red.svg)](https://redis.io/)
[![RabbitMQ](https://img.shields.io/badge/RabbitMQ-3.8+-yellow.svg)](https://www.rabbitmq.com/)
[![MySQL](https://img.shields.io/badge/MySQL-8.0+-blue.svg)](https://www.mysql.com/)

这是一个基于 **Spring Boot + Redis + RabbitMQ** 的高并发秒杀系统，针对高并发场景进行了深度优化，在保证线程安全的前提下大幅提升系统并发处理能力。

## 📊 性能提升

**JMeter压测结果：**
- 优化前QPS：800
- 优化后QPS：1900
- **性能提升：137.5%**

## ✨ 核心特性

### 🔐 安全保障
- **分布式Session**：基于Redis实现用户会话共享
- **密码安全**：双重MD5加密保护用户密码
- **接口隐藏**：动态生成秒杀接口地址
- **验证码防护**：算术验证码防止恶意攻击
- **频率限制**：接口防刷机制保护系统稳定

### ⚡ 性能优化
- **页面缓存**：减少数据库查询频率
- **对象缓存**：热点数据缓存到Redis
- **页面静态化**：前后端分离提升响应速度
- **预减库存**：Redis预减减少数据库压力
- **内存标记**：减少Redis访问次数
- **异步下单**：RabbitMQ消息队列解耦业务

### 🏗️ 系统架构
- **微服务设计**：模块化开发，职责分离
- **消息队列**：异步处理提升并发能力
- **缓存策略**：多级缓存优化性能
- **数据库优化**：连接池和索引优化

## 🛠️ 技术栈

| 技术 | 版本 | 说明 |
|------|------|------|
| Spring Boot | 2.6.5 | 企业级开发框架 |
| MySQL | 8.0+ | 关系型数据库 |
| Redis | 6.0+ | 高性能缓存数据库 |
| RabbitMQ | 3.8+ | 消息队列中间件 |
| MyBatis Plus | 3.5.1 | 数据访问层框架 |
| Thymeleaf | - | 服务端模板引擎 |
| Bootstrap | - | 前端UI框架 |

## 📋 系统功能

### 👤 用户模块
- 用户注册与登录
- 分布式会话管理
- 用户信息管理

### 📦 商品模块
- 商品列表展示
- 商品详情查看
- 秒杀商品管理

### ⚡ 秒杀模块
- 秒杀活动管理
- 库存实时监控
- 秒杀结果查询

### 📋 订单模块
- 订单生成与管理
- 订单详情查看
- 订单状态跟踪

## 🚀 快速开始

### 环境要求
- JDK 1.8+
- MySQL 8.0+
- Redis 6.0+
- RabbitMQ 3.8+

### 项目启动

1. **克隆项目**
   ```bash
   git clone https://github.com/your-username/seckill.git
   cd seckill
   ```

2. **配置数据库**
   - 创建数据库 `seckill`
   - 执行 `sqldoc/创建t_user.sql` 创建表结构

3. **修改配置**
   - 编辑 `src/main/resources/application.yml`
   - 配置数据库连接信息
   - 配置Redis连接信息
   - 配置RabbitMQ连接信息

4. **启动服务**
   ```bash
   mvn clean package
   java -jar target/seckill-0.0.1-SNAPSHOT.jar
   ```

5. **访问系统**
   - 登录页面：http://localhost:99/login/toLogin
   - 接口文档：http://localhost:99/doc.html

## 📊 项目结构

```
src/main/java/com/
├── config/          # 配置类
├── controller/      # 控制器层
├── service/         # 服务层
├── mapper/          # 数据访问层
├── pojo/            # 实体类
├── vo/              # 视图对象
├── util/            # 工具类
├── validator/       # 验证器
├── rabbitmq/        # 消息队列
└── exception/       # 异常处理
```

## 🔧 核心优化

### 缓存优化
```java
// Redis预减库存
redisTemplate.opsForValue().decrement("seckill:goods:" + goodsId);
```

### 消息队列
```java
// 异步处理秒杀请求
mqSender.sendSeckillMessage(JsonUtil.object2JsonStr(seckillMessage));
```

### 安全防护
```java
// 动态生成秒杀地址
String md5 = MD5Util.md5(UUIDUtil.uuid() + "123456");
redisTemplate.opsForValue().set("seckill:path:" + user.getId() + ":" + goodsId, md5, 60, TimeUnit.SECONDS);
```

## 📈 性能监控

系统内置性能监控指标：
- QPS（每秒查询率）
- 响应时间
- 缓存命中率
- 消息队列积压情况

## 🤝 贡献指南

欢迎提交 Issue 和 Pull Request 来改进项目！

1. Fork 本仓库
2. 创建特性分支：`git checkout -b feature/AmazingFeature`
3. 提交更改：`git commit -m 'Add some AmazingFeature'`
4. 推送到分支：`git push origin feature/AmazingFeature`
5. 提交 Pull Request

## 📄 许可证

本项目采用 MIT 许可证 - 查看 [LICENSE](LICENSE) 文件了解详情

## 🙋‍♂️ 联系方式

如有问题或建议，请通过以下方式联系：
- 提交 [GitHub Issue](https://github.com/your-username/seckill/issues)
- 发送邮件至：your-email@example.com

---

⭐ 如果这个项目对你有帮助，请给它一个 star！