# Combined TheHive and Cortex Production Deployment

This deployment combines both TheHive and Cortex into a single Docker Compose stack, sharing the same Elasticsearch instance for optimal resource utilization.

## Services Included

- **TheHive**: Security incident response platform
- **Cortex**: Observable analysis and active response engine
- **Cassandra**: Database backend for TheHive
- **Elasticsearch**: Indexing engine shared by both TheHive and Cortex
- **Nginx**: Reverse proxy for both applications

## Access URLs

- TheHive: `https://your-server/thehive`
- Cortex: `https://your-server/cortex`
- TheHive (direct): `http://your-server:9000`
- Cortex (direct): `http://your-server:9001`

## Prerequisites

- Docker Engine with Compose V2
- Sufficient system resources (recommended: 16GB RAM, 8 CPU cores)
- SSL certificates for Nginx (or use the provided script to generate self-signed ones)

## Installation

1. Copy `dot.env.template` to `.env` and configure the variables:
   ```bash
   cp dot.env.template .env
   # Edit .env with your values
   ```

2. Run the initialization script:
   ```bash
   cd scripts
   ./init.sh
   ```

3. Start the stack:
   ```bash
   docker compose up -d
   ```

## Configuration Notes

- Both TheHive and Cortex share the same Elasticsearch instance
- Nginx is configured to route `/thehive` to TheHive and `/cortex` to Cortex
- Direct access to services is available on ports 9000 (TheHive) and 9001 (Cortex)
- Cassandra is used exclusively by TheHive for its database needs
- Cortex jobs are stored in `./cortex/cortex-jobs`

## Resource Allocation

- Cassandra: 4GB RAM, 3 CPUs
- Elasticsearch: 5GB RAM, 4 CPUs (shared between TheHive and Cortex)
- TheHive: 4GB RAM, 4 CPUs
- Cortex: 5GB RAM, 4 CPUs
- Nginx: 1GB RAM, 2 CPUs

## Documentation

- [TheHive Documentation](https://docs.strangebee.com/thehive/)
- [Cortex Documentation](https://github.com/TheHive-Project/CortexDocs)
