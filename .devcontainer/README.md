# Development Container for Next.js Medusa Starter

This directory contains the configuration for a development container (devcontainer) that provides a consistent, fully-configured development environment for the Next.js Medusa Starter project.

## What's Included

### Development Environment
- **Node.js 20 LTS** with Corepack enabled for Yarn 3.x support
- **PostgreSQL 15** for Medusa backend database
- **Essential development tools**: git, curl, wget, vim, nano, postgresql-client

### VS Code Extensions
- TypeScript & JavaScript language support
- Tailwind CSS IntelliSense
- Prettier code formatter
- ESLint integration
- Auto Rename Tag
- Path IntelliSense
- npm IntelliSense
- React development tools
- GraphQL support
- Playwright testing tools
- Error Lens for inline error display

### Pre-configured Ports
- **8000**: Next.js frontend development server
- **9000**: Medusa backend server (when running)
- **5432**: PostgreSQL database

## Getting Started

### Prerequisites
- [Visual Studio Code](https://code.visualstudio.com/)
- [Dev Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)
- [Docker Desktop](https://www.docker.com/products/docker-desktop/)

### Setup Instructions

1. **Clone the repository** (if you haven't already):
   ```bash
   git clone https://github.com/Wolfschanze-Berlin/nextjs-starter-medusa.git
   cd nextjs-starter-medusa
   ```

2. **Open in VS Code**:
   ```bash
   code .
   ```

3. **Open in Dev Container**:
   - VS Code should automatically detect the devcontainer configuration
   - Click "Reopen in Container" when prompted, or
   - Use Command Palette (Ctrl/Cmd+Shift+P) → "Dev Containers: Reopen in Container"

4. **Wait for setup**: The container will build and install dependencies automatically

### What Happens During Setup

The devcontainer automatically:
- Builds the development environment with Node.js 20 and all required tools
- Starts a PostgreSQL database for Medusa backend development
- Enables Corepack for Yarn 3.x support
- Copies `.env.template` to `.env.local` for environment configuration
- Installs all npm dependencies
- Configures VS Code with recommended extensions and settings

## Using the Development Environment

### Starting the Frontend
```bash
npm run dev
# or
yarn dev
```
The frontend will be available at http://localhost:8000

### Database Access
The PostgreSQL database is available with these credentials:
- **Host**: `postgres` (within container) or `localhost` (from host)
- **Port**: `5432`
- **Database**: `medusa_store`
- **User**: `medusa_user`
- **Password**: `medusa_password`

### Running a Medusa Backend
If you want to run a Medusa backend alongside the frontend:

1. **Create a new Medusa project** (in a separate terminal):
   ```bash
   npx create-medusa-app@latest backend --db-url="postgresql://medusa_user:medusa_password@postgres:5432/medusa_store"
   ```

2. **Start the backend**:
   ```bash
   cd backend
   npm run dev
   ```
   The backend will be available at http://localhost:9000

### Environment Variables
The devcontainer automatically creates `.env.local` from `.env.template`. Update these variables as needed:
- `MEDUSA_BACKEND_URL`: URL of your Medusa backend (default: http://localhost:9000)
- `NEXT_PUBLIC_MEDUSA_PUBLISHABLE_KEY`: Your Medusa publishable key
- `NEXT_PUBLIC_STRIPE_KEY`: Your Stripe public key (for payment processing)

## Available Commands

```bash
# Frontend development
npm run dev          # Start development server
npm run build        # Build for production
npm run start        # Start production server
npm run lint         # Run ESLint

# Database operations (using postgresql-client)
psql -h postgres -U medusa_user -d medusa_store  # Connect to database

# Package management
yarn install        # Install dependencies
yarn add <package>   # Add new dependency
```

## Troubleshooting

### Container Won't Start
- Ensure Docker Desktop is running
- Try rebuilding the container: Command Palette → "Dev Containers: Rebuild Container"

### Port Conflicts
If ports 8000, 9000, or 5432 are already in use on your host machine:
1. Stop the conflicting services, or
2. Update the port mappings in `.devcontainer/docker-compose.yml`

### Dependencies Issues
If you encounter dependency issues:
```bash
# Clear node_modules and reinstall
rm -rf node_modules
npm install
```

### Database Connection Issues
Ensure the PostgreSQL service is running:
```bash
# Check if postgres container is running
docker ps | grep postgres
```

## Customization

### Adding VS Code Extensions
Edit `.devcontainer/devcontainer.json` and add extension IDs to the `extensions` array.

### Modifying Environment
- **System packages**: Add to `Dockerfile`
- **Node version**: Update the node feature version in `devcontainer.json`
- **Database configuration**: Modify environment variables in `docker-compose.yml`

### Performance Optimization
For better performance on Windows/macOS, consider using named volumes instead of bind mounts for node_modules:

```yaml
# Add to docker-compose.yml volumes section
node_modules:/workspace/node_modules
```

## Support

For issues specific to this devcontainer setup, please check:
1. [VS Code Dev Containers documentation](https://code.visualstudio.com/docs/remote/containers)
2. [Project README](../README.md) for general setup information
3. [Medusa documentation](https://docs.medusajs.com/) for backend-related questions