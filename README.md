# Blender-MCP-Docker

从 [ahujasid/blender-mcp](https://github.com/ahujasid/blender-mcp) 构建多架构镜像并推送到 Docker Hub。

## 镜像

```
arcticfox520/blender-mcp:latest        # 上游 main 最新一次成功构建
arcticfox520/blender-mcp:sha-<7位>     # 上游提交短 SHA
```

平台：`linux/amd64`、`linux/arm64`。

```bash
docker run --rm -i --add-host=host.docker.internal:host-gateway \
  -e BLENDER_HOST=host.docker.internal -e BLENDER_PORT=9876 \
  arcticfox520/blender-mcp:latest
```

Blender 需运行在宿主机，容器内不含 Blender。
