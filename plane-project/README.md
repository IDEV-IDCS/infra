# Plane Project Management Setup

## Overview
Plane is a modern project management tool with issues, sprints, cycles, and pages.

## Official Installation (Recommended)

### Method 1: One-Command Install (Commercial Edition)
```bash
curl -fsSL https://prime.plane.so/install/ | sh -
```

### Method 2: Community Edition Setup
```bash
# Create directory
mkdir plane-selfhost && cd plane-selfhost

# Download setup script
curl -fsSL -o setup.sh https://github.com/makeplane/plane/releases/latest/download/setup.sh

# Make executable and run
chmod +x setup.sh
./setup.sh
```

## Configuration for External Services

After installation, configure external services:

### 1. Database Configuration
Edit the generated `plane.env` file:
```env
DATABASE_URL=postgresql://username:password@your-postgres-host:5432/plane_db
```

### 2. Redis Configuration
```env
REDIS_URL=redis://your-redis-host:6379/0
```

### 3. S3 Storage Configuration
```env
USE_MINIO=0
AWS_REGION=ap-south-1
AWS_ACCESS_KEY_ID=your-access-key
AWS_SECRET_ACCESS_KEY=your-secret-key
AWS_S3_BUCKET_NAME=qpg-plane
```

### 4. Domain Configuration
```env
WEB_URL=https://plane.devcode.live
```

## OIDC Setup with Keycloak

1. Deploy Plane using official method
2. Access admin panel: `https://plane.devcode.live/god-mode/authentication/oidc`
3. Configure OIDC settings:
   - **Client ID**: `plane`
   - **Client Secret**: From Keycloak
   - **Authorize URL**: `https://keycloak.devcode.live/realms/devcode/protocol/openid-connect/auth`
   - **Token URL**: `https://keycloak.devcode.live/realms/devcode/protocol/openid-connect/token`
   - **User Info URL**: `https://keycloak.devcode.live/realms/devcode/protocol/openid-connect/userinfo`

## Deployment in Dokploy

1. Use the official Plane installation method
2. Configure domain `plane.devcode.live` in Dokploy
3. Update environment variables for external services
4. Enable SSL certificates

## Features
- Issue tracking
- Sprint planning  
- Kanban boards
- Pages (documentation)
- Analytics
- Team collaboration
- OIDC authentication
