# OpenWrt x86_64

这是一个用于构建 OpenWrt x86_64 固件的配置仓库，当前构建 OpenWrt 24.10.5。

固件包含以下网络工具：PassWall、OpenClash、SSR Plus、NPS 客户端和哪吒监控 Agent。

## 目录结构

```text
.
├── .github/workflows/build.yml
├── config/x86_64.config
├── feeds.conf.default
└── README.md
```

## 本地构建

需要 Linux 环境、Git、编译工具链以及约 20 GB 可用磁盘空间。

```bash
git clone https://github.com/openwrt/openwrt.git
cd openwrt
git checkout v24.10.5
cp ../x86/config/x86_64.config .config
cp ../x86/feeds.conf.default feeds.conf.default
./scripts/feeds update -a
./scripts/feeds install -a
make defconfig
make -j$(nproc)
```

生成的固件位于 `bin/targets/x86/64/`。

## GitHub Actions

推送到 `main` 分支或手动运行 `Build OpenWrt` workflow 后，构建产物会作为 Actions artifact 上传。发布版本和构建选项分别由 workflow 与 `config/x86_64.config` 控制。