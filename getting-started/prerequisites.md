# Prerequisites

Before you start developing with Munja LST, ensure you have the following tools and dependencies installed.

## Required Tools

### Node.js and pnpm

**Node.js**: Version 20 or higher

```bash
# Check Node.js version
node --version

# Install via nvm (recommended)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
nvm install 20
nvm use 20

# Or download from nodejs.org
# https://nodejs.org/
```

**pnpm**: Version 10.15.1 or higher

```bash
# Install pnpm
npm install -g pnpm@10.15.1

# Verify installation
pnpm --version
```

### Foundry

Foundry is required for smart contract development.

```bash
# Install Foundry
curl -L https://foundry.paradigm.xyz | bash

# Run foundryup to install forge, cast, anvil, and chisel
foundryup

# Verify installation
forge --version
cast --version
```

### Rust

Rust 1.83+ with nightly toolchain is required for oracle development.

```bash
# Install Rust
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

# Install nightly toolchain
rustup toolchain install nightly

# Verify installation
rustc --version
cargo --version
```

### SP1 Toolchain (For Oracle Development)

SP1 is required for zero-knowledge proof generation.

```bash
# Install SP1
curl -L https://sp1.succinct.xyz | bash

# Run sp1up to install the toolchain
sp1up

# Verify installation
sp1 --version
```

### PostgreSQL (Optional)

Required if using PostgreSQL for oracle checkpoint storage.

```bash
# macOS (via Homebrew)
brew install postgresql@16
brew services start postgresql@16

# Ubuntu/Debian
sudo apt-get install postgresql-16

# Verify installation
psql --version
```

**sqlx-cli** for database migrations:

```bash
cargo install sqlx-cli --no-default-features --features postgres
```

### Docker and Docker Compose (Recommended)

Docker is recommended for running services in containers.

```bash
# Install Docker Desktop (includes Docker Compose)
# https://www.docker.com/products/docker-desktop/

# Or install Docker and Docker Compose separately
# Linux: https://docs.docker.com/engine/install/
# Docker Compose: https://docs.docker.com/compose/install/

# Verify installation
docker --version
docker compose version
```

## Optional Tools

### AWS CLI (For S3 Storage)

Required if using S3 for oracle checkpoint storage.

```bash
# Install AWS CLI
# https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

# Configure credentials
aws configure

# Verify installation
aws --version
```

### Git

```bash
# Most systems have git pre-installed
git --version

# If not installed:
# macOS: xcode-select --install
# Ubuntu/Debian: sudo apt-get install git
```

### Code Editor

Recommended editors with good Solidity and Rust support:

- **Visual Studio Code** with extensions:
  - Solidity (by Juan Blanco)
  - rust-analyzer
  - Prettier
  - ESLint
- **Cursor** (AI-powered VS Code fork)
- **IntelliJ IDEA** with Rust and Solidity plugins

## System Requirements

### Minimum Requirements

- **CPU**: 4 cores
- **RAM**: 8 GB
- **Storage**: 50 GB available
- **OS**: macOS, Linux, or Windows (WSL2)

### Recommended for Oracle Proving

- **CPU**: 8+ cores
- **RAM**: 16+ GB
- **Storage**: 100+ GB SSD
- **GPU** (optional): NVIDIA GPU with CUDA for faster proving

## Network Access

Ensure you have access to the following:

### RPC Endpoints

**Cosmos Chain**:
- Default: `https://rpc.mitosis.org/cc/rpc`
- Or your own Cosmos node

**EVM Chain** (Arbitrum, Ethereum, etc.):
- Public RPC: `https://arb1.arbitrum.io/rpc`
- Or premium providers (Alchemy, Infura, Quicknode)

### GitHub

```bash
# Verify SSH access to GitHub
ssh -T git@github.com

# Or configure HTTPS with credentials
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

## Verifying Installation

Run this verification script to check all prerequisites:

```bash
#!/bin/bash

echo "Checking prerequisites..."

# Node.js
if command -v node &> /dev/null; then
    echo "✓ Node.js $(node --version)"
else
    echo "✗ Node.js not found"
fi

# pnpm
if command -v pnpm &> /dev/null; then
    echo "✓ pnpm $(pnpm --version)"
else
    echo "✗ pnpm not found"
fi

# Foundry
if command -v forge &> /dev/null; then
    echo "✓ Foundry $(forge --version | head -n1)"
else
    echo "✗ Foundry not found"
fi

# Rust
if command -v cargo &> /dev/null; then
    echo "✓ Rust $(rustc --version)"
else
    echo "✗ Rust not found"
fi

# SP1 (optional)
if command -v sp1 &> /dev/null; then
    echo "✓ SP1 $(sp1 --version)"
else
    echo "⚠ SP1 not found (optional for oracle development)"
fi

# Docker
if command -v docker &> /dev/null; then
    echo "✓ Docker $(docker --version)"
else
    echo "⚠ Docker not found (optional but recommended)"
fi

# PostgreSQL (optional)
if command -v psql &> /dev/null; then
    echo "✓ PostgreSQL $(psql --version)"
else
    echo "⚠ PostgreSQL not found (optional)"
fi

echo ""
echo "Verification complete!"
```

Save as `check-prereqs.sh`, make executable, and run:

```bash
chmod +x check-prereqs.sh
./check-prereqs.sh
```

## Environment Variables

Create a `.env` file in your project root (you'll populate this during installation):

```bash
# Cosmos RPC
RPC_URL=https://rpc.mitosis.org/cc/rpc

# EVM RPC
EVM_RPC_URL=https://arb1.arbitrum.io/rpc
CHAIN_ID=42161

# Private keys (for deployment and oracle operations)
PRIVATE_KEY=
ORACLE_FEEDER_KEY=

# Database (if using PostgreSQL)
DATABASE_URL=postgresql://user:password@localhost:5432/munja_oracle

# Storage (for oracle)
STORAGE=postgres
# Or: STORAGE=s3
# S3_BUCKET=my-bucket
# S3_PREFIX=checkpoints/
# AWS_REGION=us-east-1
```

**Security Note**: Never commit `.env` files to version control. Add to `.gitignore`:

```bash
echo ".env" >> .gitignore
echo ".env.local" >> .gitignore
```

## Next Steps

Once you have all prerequisites installed:

1. [Installation Guide](installation.md) - Clone and setup the project
2. [Quick Start](quick-start.md) - Run your first local deployment
3. [Development Setup](../development/setup.md) - Configure your development environment

## Troubleshooting

### Issue: Node version conflicts

Use `nvm` to manage multiple Node.js versions:

```bash
nvm install 20
nvm use 20
nvm alias default 20
```

### Issue: Foundry installation fails

Try installing from source:

```bash
git clone https://github.com/foundry-rs/foundry
cd foundry
cargo install --path ./cli --profile local --force
```

### Issue: SP1 toolchain not found

Ensure your shell profile is updated:

```bash
# Add to ~/.bashrc, ~/.zshrc, or equivalent
export PATH="$HOME/.sp1/bin:$PATH"

# Reload shell
source ~/.bashrc  # or source ~/.zshrc
```

### Issue: PostgreSQL connection refused

Start PostgreSQL service:

```bash
# macOS
brew services start postgresql@16

# Linux (systemd)
sudo systemctl start postgresql

# Check status
brew services list  # macOS
sudo systemctl status postgresql  # Linux
```

### Issue: Permission denied for Docker

Add your user to docker group (Linux):

```bash
sudo usermod -aG docker $USER
newgrp docker
```

## Getting Help

If you encounter issues:

1. Check the [Troubleshooting Guide](../appendix/troubleshooting.md)
2. Search [GitHub Issues](https://github.com/your-org/munja-lst/issues)
3. Ask in the community Discord/Telegram
4. Create a new GitHub issue with:
   - Operating system and version
   - Tool versions (`check-prereqs.sh` output)
   - Error messages and logs
   - Steps to reproduce
