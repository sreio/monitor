# monitor

## grafana 模板

### node

- `github`: https://github.com/prometheus/node_exporter
- `grafana`: https://grafana.com/grafana/dashboards/8919-node-exporter-dashboard-20240520-tensuns/

### nginx-exporter

- `github`: https://github.com/nginx/nginx-prometheus-exporter

### mysql-exporter

- `github`: https://github.com/prometheus/mysqld_exporter
- `grafana`:https://grafana.com/grafana/dashboards/17320-1-mysqld-exporter-dashboard/

## 依赖

> 需要安装 docker 和 docker-compose

```bash
# 主节点启动所有
docker-compose up -d
# 停止删除
docker-compose down
# 从节点启动 Node Exporter
docker-compose up -d node-exporter nginx-exporter

# 重载prometheus
curl -X POST http://localhost:8090/-/reload
```


## debian 安装 docker
```bash
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common gnupg
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io

# 查看docker 服务状态
sudo systemctl status docker

# 配置 Docker 免 sudo（可选）
sudo usermod -aG docker $USER
newgrp docker

# 验证 Docker 安装
docker --version
```

## debian 安装 docker-compose
```bash
sudo apt -y install jq
# 获取最新的 Docker Compose 版本
COMPOSE_VERSION=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | jq -r .tag_name)
# 下载 Docker Compose
sudo curl -L "https://github.com/docker/compose/releases/download/${COMPOSE_VERSION}/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
# 置执行权限
sudo chmod +x /usr/local/bin/docker-compose
# 验证 Docker Compose 安装
docker-compose --version
```

## ubuntu 安装 docker
```bash
sudo apt install -y apt-transport-https ca-certificates curl gnupg lsb-release software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io
# 启动 Docker 并设为开机自启
sudo systemctl start docker
sudo systemctl enable docker
# 查看 Docker 服务状态
sudo systemctl status docker

# 配置 Docker 免 sudo（可选）
sudo usermod -aG docker $USER
newgrp docker

# 验证 Docker 安装
docker --version
```

## ubuntu 安装 docker-compose
```bash
sudo apt install -y jq
# 获取最新版本号，例如 v2.20.2
COMPOSE_VERSION=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | jq -r .tag_name)

# 下载 Docker Compose（请注意：docker-compose V2 已作为插件发布，如果需要独立二进制文件，此命令适用）
sudo curl -L "https://github.com/docker/compose/releases/download/${COMPOSE_VERSION}/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

# 赋予可执行权限
sudo chmod +x /usr/local/bin/docker-compose

docker-compose --version
```


## centos9 安装 docker
```bash
sudo dnf install -y yum-utils device-mapper-persistent-data lvm2
sudo dnf config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
sudo dnf install -y docker-ce docker-ce-cli containerd.io

# 启动 Docker 服务
sudo systemctl start docker
# 查看 Docker 服务状态
sudo systemctl status docker

# 配置 Docker 免 sudo（可选）
sudo usermod -aG docker $USER
newgrp docker

# 验证 Docker 安装
docker --version
```

## centos9 安装 docker-compose
```bash
sudo dnf install -y jq
COMPOSE_VERSION=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | jq -r .tag_name)
sudo curl -L "https://github.com/docker/compose/releases/download/${COMPOSE_VERSION}/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version
```


## centos7 安装 docker
```bash
# 安装依赖
sudo yum install -y yum-utils device-mapper-persistent-data lvm2
# 添加 Docker 官方仓库
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
# 安装 Docker
sudo yum install -y docker-ce docker-ce-cli containerd.io
# 启动 Docker
sudo systemctl start docker
# 开机自启
sudo systemctl enable docker
# 配置 Docker 免 sudo（可选）
sudo usermod -aG docker $USER
newgrp docker  # 让用户组立即生效，或重新登录
# 验证 Docker 安装
docker --version
```

## centos7 安装 docker-compose
```bash
# 安装 jq 用于解析 JSON
sudo yum install -y jq curl
# 获取最新版本号
COMPOSE_VERSION=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | jq -r .tag_name)
# 下载 docker-compose 可执行文件
sudo curl -L "https://github.com/docker/compose/releases/download/${COMPOSE_VERSION}/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
# 添加执行权限
sudo chmod +x /usr/local/bin/docker-compose
# 验证版本
docker-compose --version

```
