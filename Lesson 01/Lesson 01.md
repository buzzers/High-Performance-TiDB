# Lesson 01

## 准备环境

```bash
# 设置 Go 版本
export VERSION="1.15"
export OS="linux"
export ARCH="amd64"

# 安装 Go
curl -sfL "https://golang.org/dl/go$VERSION.$OS-$ARCH.tar.gz" -o "go$VERSION.$OS-$ARCH.tar.gz"
tar -C /usr/local -xzf go$VERSION.$OS-$ARCH.tar.gz

export PATH=$PATH:/usr/local/go/bin
```

## 修改代码

克隆 TiDB 存储库。

```bash
git clone "https://github.com/pingcap/tidb.git"
cd tidb
git checkout -b Branch_v4.0.4 v4.0.4
```

打开 `executor/simple.go`，定位到函数 `func (e *SimpleExec) executeBegin(ctx context.Context, s *ast.BeginStmt) error`。在最后返回语句前添加 `logutil.Logger(ctx).Info("hello transaction")`。

## 编译

执行如下语句编译。

```bash
make
```

## 部署

```bash
# 安装 TiUP
curl --proto '=https' --tlsv1.2 -sSf https://tiup-mirrors.pingcap.com/install.sh | sh

# 启动 TiDB
tiup playground v4.0.4 --db.binpath ~/tidb/bin/tidb-server
```
