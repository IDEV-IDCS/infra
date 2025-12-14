# Plane Project Management Setup

## Overview
Plane is a modern project management tool with issues, sprints, cycles, and pages.

## Resource Usage
- **RAM**: ~300MB total
- **Services**: Web, API, Worker, PostgreSQL, Redis, MinIO

## Deployment

1. **Update environment variables in `.env`:**
   ```bash
   # Generate a secure secret key (32+ characters)
   SECRET_KEY=your-secure-secret-key-here
   
   # Update MinIO credentials
   MINIO_ROOT_PASSWORD=your-secure-password
   AWS_SECRET_ACCESS_KEY=your-secure-password
   ```

2. **Deploy in Dokploy:**
   ```bash
   cd plane-project
   docker-compose up -d
   ```

3. **Configure domains in Dokploy:**
   - `plane.devcode.live` → plane-web:3000
   - `plane-space.devcode.live` → plane-space:3000 (optional)

## First Setup
1. Access `https://plane.devcode.live`
2. Create admin account
3. Set up your first workspace
4. Invite team members

## Features
- Issue tracking
- Sprint planning
- Kanban boards
- Pages (documentation)
- Analytics
- Team collaboration
