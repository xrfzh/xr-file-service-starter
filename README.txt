导入依赖（用哪个第三方文件上传服务则导入对应的依赖就行（推荐），全导入也行）：
<dependency>
    <groupId>io.github.xrfzh.cn</groupId>
    <artifactId>aliyun-file-service-starter</artifactId>
    <version>2.2.0-RELEASE</version>
</dependency>
<dependency>
    <groupId>io.github.xrfzh.cn</groupId>
    <artifactId>minio-file-service-starter</artifactId>
    <version>2.2.0-RELEASE</version>
</dependency>
<dependency>
    <groupId>io.github.xrfzh.cn</groupId>
    <artifactId>tencentcloud-file-service-starter</artifactId>
    <version>2.2.0-RELEASE</version>
</dependency>
<dependency>
    <groupId>io.github.xrfzh.cn</groupId>
    <artifactId>qiniuyun-file-service-starter</artifactId>
    <version>2.2.0-RELEASE</version>
</dependency>
<dependency>
    <groupId>io.github.xrfzh.cn</groupId>
    <artifactId>fastdfs-file-service-starter</artifactId>
    <version>2.2.0-RELEASE</version>
</dependency>
<dependency>
    <groupId>io.github.xrfzh.cn</groupId>
    <artifactId>xr-common-utils</artifactId>
    <version>2.2.0-RELEASE</version>
</dependency>
——————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————
application.yml 配置如下：

minio:
  accessKey: your accessKey
  secretKey: your secretKey
  endPoint: http://42.192.150.29:9000
  bucketName: fzh-public

aliyun:
  keyId: your keyId
  keySecret: your keySecret
  endPoint: oss-cn-shenzhen.aliyuncs.com
  bucketName: weiyijian-upload
  moduleName: 文件夹名称（如：java）

tencent-cloud:
  secretId: your secretId
  secretKey: your secretKey
  filePath: https://weiyijian-upload-1312337739.cos.ap-beijing.myqcloud.com
  bucketName: weiyijian-upload-1312337739
  regionName: ap-beijing
  moduleName: 文件夹名称（如：java）

qiniuyun:
  accessKey: your accessKey
  secretKey: your secretKey
  domainOfBucket: qiniuyun.fzhxfw.xyz
  bucketName: weiyijian-upload
  # [{'zone0':'华东'}, {'zone1':'华北'},{'zone2':'华南'},{'zoneNa0':'北美'},{'zoneAs0':'其他'}]
  zoneName: zone2
  # 链接过期时间，单位是秒，3600代表1小时，-1代表永不过期
  expireInSeconds: -1

fdfs:
  # 服务器地址
  tracker-list: 服务器IP:22122
  # 连接超时
  connect-timeout: 60
  # 读取时间
  so-timeout: 60
  # 生成缩略图参数
  thumb-image:
    width: 150
    height: 150
    
——————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————

新建一个扫描组件的配置类如下：

package com.example.test.config;

import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;

@Configuration
@ComponentScan("com.xr")
public class initConfig {

}

注入依赖如下（其他服务命名规则类似于阿里云服务）：
@Resource
private AliyunFileService aliyunFileService;

根据IDEA提示调用对应方法即可！！！
