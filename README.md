# DDNS 动态域名解析

支持 阿里云 IPv4 解析。

## 安装运行环境

```bash
cd [安装目录]
python -m venv venv
. venv/bin/activate
pip install -r requirements.txt
```

## 编写配置文件

编辑项目根目录的 `config.yaml`

### 示例 1：1 个主域名和 1 个子域名

```yaml
alidns:
  key: ***********************
  secret: ***********************
  domains:
    - DomainName: example.com
      RR: 
        - www
```

### 示例 2：1 个主域名和多个子域名

```yaml
alidns:
  key: ***********************
  secret: ***********************
  domains:
    - DomainName: example.com
      RR:
        - www
        - '@'
```

### 示例 3：多个主域名和多个子域名

```yaml
alidns:
  key: ***********************
  secret: ***********************
  domains:
    - DomainName: example.com
      RR:
        - www
        - '@'
    - DomainName: example2.com
      RR:
        - www
        - '@'
```

## crontab 设置

在 `/etc/crontab` 文件添加下面代码

```crontab
*/5 * * * * root cd ~/DDNS && . venv/bin/activate && python src/alidns/ipv4.py
```