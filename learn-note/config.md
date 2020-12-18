# 数据流向

.env  -> docker-compose.yml  -> Dockerfile

# 定义

## 临时变量

在 DockerFile 中定义变量。

```dock
# 无默认值
ARG LARADOCK_PHP_VERSION

# 有默认值
ARG BASE_IMAGE_TAG_PREFIX=latest

# 使用变量
FROM laradock/php-fpm:${BASE_IMAGE_TAG_PREFIX}-${LARADOCK_PHP_VERSION}
```

> ARG 定义的变量只存在于 build 阶段，build 后变量将会消失，适用于环境构建所用的变量声明。



## 环境变量

```dock
# 变量默认值
ARG LARADOCK_PHALCON_VERSION
ENV LARADOCK_PHALCON_VERSION ${LARADOCK_PHALCON_VERSION}

# 有默认值
ENV DEBIAN_FRONTEND noninteractive

# 其他定义方式：= 赋值，一行多个
ENV DEBIAN_FRONTEND=noninteractive DEBIAN_FRONTEND_2=noninteractive
```

> ENV 定义的环境变量一直存在，不会消失，适用于容器程序所用的变量声明。

```do
# 示例一
ENV NODE_VERSION 7.2.0

RUN curl -SLO "https://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.xz" \
  && curl -SLO "https://nodejs.org/dist/v$NODE_VERSION/SHASUMS256.txt.asc"
```



# 配置

## docker-compose.yml

```yaml
# ....

services:
	php-fpm:
		build:
			args:
				- LARADOCK_PHP_VERSION=${PHP_VERSION}
				- VERSION=${PHP_FPM_VERSION}
				# 变量名=${.env 文件中的变量}

# ...
```





## .env

```
PHP_VERSION=7.3

PHP_FPM_VERSION=3
```



