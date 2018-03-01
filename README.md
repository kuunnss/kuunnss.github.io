# 简单实现Redis读写分离（一主一从为例）

## 1.安装Redis

```markdown
$ wget http://download.redis.io/releases/redis-4.0.8.tar.gz
$ tar xzf redis-4.0.8.tar.gz
$ cd redis-4.0.8
$ make
```
## 2.拷贝Redis.conf 并进行配置
进入redis安装文件夹
```markdown
cp redis.conf redis2 conf
```
### 配置 端口号
```markdown
vi Redis2.conf 
```
```markdown
port 6380
```
```markdown
pidfile /var/run/redis_6380.pid
```
### 配置从机
```markdown
# slaveof <masterip> <masterport>
slave of 127.0.0.1:6379
```
## 3.启动主从Redis
### 启动主机
```markdown
cd src
./redis-server ../redis.conf
```
### 启动从机
```markdown
./redis-server ../redis2.conf
```
此时 主机上显示从机已连接
## 4.连接主从Redis 并测试
### 连接主机
```markdown
./redis-cli -h 127.0.0.1 -p 6379
```
### 连接从机
```markdown
./redis-cli -h 127.0.0.1 -p 6380
```
### 主机写入
```markdown
set key1 value1
```
### 从机读
```markdown
get key1
```
End
