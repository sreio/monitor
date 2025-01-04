# monitor

## 依赖

> 需要安装 docker 和 docker-compose

```bash
# 主节点启动所有
docker-compose up -d
# 停止删除
docker-compose down
# 从节点启动 Node Exporter
docker-compose up -d node-exporter
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


### 参考

- https://cloud.tencent.com/developer/article/1923703
- https://github.com/feiyu563/PrometheusAlert


### 其他

- https://grafana.com/grafana/dashboards/17320-1-mysqld-exporter-dashboard/
- https://sheldon-lu.github.io/sheldon_Gitbook/Introduction.html
- https://www.cnblogs.com/hahaha111122222/p/13724172.html