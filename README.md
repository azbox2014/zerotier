# ZeroTierOne Docker Image Builder

A project for building multi-architecture Docker images of ZeroTierOne with automated CI/CD pipeline via GitHub Actions and publishing to GitHub Container Registry (GHCR).

## Features

- ✅ Multi-architecture support (linux/amd64, linux/arm64)
- ✅ Automated CI/CD pipeline
- ✅ GitHub Actions-based build triggers
- ✅ Image publishing to GitHub Container Registry
- ✅ Version-specific builds

## Usage

### Triggering Builds

1. Navigate to the Actions tab in your GitHub repository
2. Select the "Build ZeroTierOne Image (Tag)" workflow
3. Click "Run workflow"
4. Enter the ZeroTierOne version number (e.g., 1.14.0)
5. Click "Run workflow" to start the build process

### Pulling Images

After the build completes, pull images from GitHub Container Registry:

```bash
# Pull specific version
docker pull ghcr.io/azbox2014/zerotier-one:1.14.0

# Pull latest version
docker pull ghcr.io/azbox2014/zerotier-one:latest
```

### Running Container

```bash
docker run -d \
  --name zerotier-one \
  --device=/dev/net/tun \
  --cap-add=NET_ADMIN \
  --cap-add=SYS_ADMIN \
  --cap-add=NET_RAW \
  -v /var/lib/zerotier-one:/var/lib/zerotier-one \
  ghcr.io/azbox2014/zerotier-one:latest
```

## Build Configuration

### Environment Variables

- `REGISTRY`: Docker registry URL (default: ghcr.io)
- `IMAGE_NAME`: Image name (default: zerotier-one)

### Build Platforms

- linux/amd64
- linux/arm64

### Build Parameters

- `VERSION`: ZeroTierOne version number (required parameter)

## Project Structure

```
.
├── .github/
│   └── workflows/
│       └── build.yml          # GitHub Actions workflow configuration
└── .gitignore                 # Git ignore file configuration
```

## Workflow Steps

1. **Checkout**: Checkout the repository
2. **Clone ZeroTierOne**: Clone ZeroTierOne source code
3. **Set up QEMU**: Configure QEMU for multi-architecture builds
4. **Set up Buildx**: Configure Docker Buildx
5. **Login to GHCR**: Authenticate to GitHub Container Registry
6. **Build and Push**: Build and push multi-architecture images

## License

This project follows the ZeroTierOne license.

## Related Links

- [ZeroTierOne Official Repository](https://github.com/zerotier/ZeroTierOne)
- [ZeroTier Official Website](https://www.zerotier.com/)
- [GitHub Container Registry](https://ghcr.io)

## Notes

- Configure the `AGH_TOKEN` secret in GitHub repository settings for pushing to GHCR
- Build process requires time, please wait patiently
- Ensure your GitHub account has permissions to access GHCR