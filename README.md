平台：`linux/amd64`、`linux/arm64`。

## 触发

| 方式 | 说明 |
| --- | --- |
| 手动 | 可选 `ref`：分支 / 标签 / 完整 40 位 commit SHA，默认 `main` |
| 定时 | 每周日 06:00 UTC，获取基础镜像安全更新 |

只推 Docker Hub；上游 Dockerfile 的 `FROM`（`ghcr.io/astral-sh/uv`）仍从 GHCR 拉取。非 `main` 的 ref 只产出 `sha-<7位>`，不移动 `latest`。构建成功后本文件同步为 Docker Hub 仓库描述。

## 使用

先在 Blender 中启用 MCP 插件并启动服务：3D 视图 `N` 面板 → BlenderMCP → Connect to MCP server。插件只监听 `localhost:9876`。

```bash
# Linux：必须共享宿主网络，否则连不到只监听 127.0.0.1 的插件
docker run --rm -i --network=host \
  -e BLENDER_HOST=127.0.0.1 -e BLENDER_PORT=9876 \
  arcticfox520/blender-mcp:latest

# Docker Desktop（macOS / Windows）
docker run --rm -i --add-host=host.docker.internal:host-gateway \
  -e BLENDER_HOST=host.docker.internal -e BLENDER_PORT=9876 \
  arcticfox520/blender-mcp:latest
```

容器内不含 Blender。`Could not find a Blender addons folder` 是容器里读不到宿主机 Blender 配置，可忽略；`Connection refused` 表示 9876 未监听或不可达，先在宿主机用 `ss -ltnp | grep 9876` 确认。
