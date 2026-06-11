

```mermaid
graph LR
    CloudNative --> SRE
    CloudNative --> DEV

    SRE --- Observe
    SRE --- Linux
    SRE --- K8S
    SRE --- Devops
    SRE --- Alicloud

    DEV --- springboot3.x
    DEV --- Redis
    DEV --- Mysql
    DEV --- Java17
```
