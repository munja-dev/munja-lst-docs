# Getting Started

Welcome to the Munja LST development guide. This section will help you get up and running with the protocol.

## What You'll Learn

This getting started guide covers:

1. **Prerequisites** - Install required tools and dependencies
2. **Installation** - Clone and setup the project
3. **Quick Start** - Run your first local deployment and tests

## Quick Navigation

### For Smart Contract Developers

If you're primarily interested in smart contract development:

1. ✅ [Prerequisites](prerequisites.md) - Install Foundry, Node.js, pnpm
2. ✅ [Installation](installation.md) - Clone repo and install dependencies
3. ✅ [Quick Start](quick-start.md) - Run tests and deploy locally
4. 📖 [Contracts Overview](../contracts/overview.md) - Understand contract architecture
5. 🛠️ [Development Workflow](../development/workflow.md) - Day-to-day development

### For Oracle Developers

If you're working on the oracle system:

1. ✅ [Prerequisites](prerequisites.md) - Install Rust, SP1, PostgreSQL
2. ✅ [Installation](installation.md) - Setup oracle services
3. ✅ [Quick Start](quick-start.md) - Run prover and feeder
4. 📖 [Oracle Overview](../oracle/overview.md) - Understand oracle architecture
5. 🛠️ [Prover Setup](../oracle/prover/README.md) - Configure and run prover
6. 🛠️ [Feeder Setup](../oracle/feeder/README.md) - Configure and run feeder

### For Full-Stack Developers

If you're working on the entire system:

1. ✅ [Prerequisites](prerequisites.md) - Install all tools
2. ✅ [Installation](installation.md) - Full monorepo setup
3. ✅ [Quick Start](quick-start.md) - Run all services
4. 📖 [Development Setup](../development/setup.md) - Configure development environment
5. 🛠️ [Development Workflow](../development/workflow.md) - Work with the monorepo

## Estimated Time

- **Prerequisites**: 15-30 minutes
- **Installation**: 10-20 minutes
- **Quick Start**: 15-30 minutes

**Total**: ~1 hour for complete setup

## System Requirements

Before starting, ensure your system meets these requirements:

### Minimum

- **OS**: macOS, Linux, or Windows (WSL2)
- **CPU**: 4 cores
- **RAM**: 8 GB
- **Storage**: 50 GB

### Recommended (for oracle proving)

- **CPU**: 8+ cores
- **RAM**: 16+ GB
- **Storage**: 100+ GB SSD
- **GPU**: NVIDIA GPU with CUDA (optional, for faster proving)

## What's Included

The Munja LST monorepo includes:

```
munja-lst/
├── contracts/     # Smart contracts (Solidity)
├── oracle/        # Oracle system (Rust)
│   ├── lib/       # Verification library
│   ├── program/   # zkVM program
│   ├── prover/    # Proof generation service
│   └── feeder/    # Contract feeding service
├── app/           # Frontend (Next.js)
├── indexer/       # Event indexer (Ponder)
├── operator/      # Automation service
└── common/        # Shared packages
```

## Need Help?

- 📖 Check the [FAQ](../appendix/faq.md)
- 🐛 See [Troubleshooting](../appendix/troubleshooting.md)
- 💬 Ask in the community Discord/Telegram
- 🐙 Create a [GitHub Issue](https://github.com/your-org/munja-lst/issues)

## Next Steps

Ready to begin? Start with the [Prerequisites Guide](prerequisites.md).
