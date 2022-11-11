# spring-boot-logging-example

验证ECS fargate模式下应用日志收集，主要实现如下两种方式：

* Task日志落盘方式写入到efs：ecs/task_definition_log_to_efs.json
* Task日志写到标准输出，通过firelens落盘到S3: ecs/task_definition_log_to_s3.json

# 使用方式

0. 编译Springboot应用，构建docker image并上传至ECR

1. 创建ECS集群

2. 命令行方式创建task（请留意升级aws命令工具到最近版本）
```
aws ecs register-task-definition \
    --cli-input-json file://<path_to_json_file>/task_definition.json
```
3. 部署service至ecs集群

4. 请求服务接口`/rest`，前往efs/s3查看日志

5. 通过Log Hub方案集中采集efs/s3中的日志

# REFs

1. https://docs.aws.amazon.com/AmazonECS/latest/developerguide/firelens-taskdef.html