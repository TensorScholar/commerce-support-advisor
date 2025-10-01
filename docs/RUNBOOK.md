# Operations Runbook

## Common Operations

### Starting Services
```bash
# Development
pnpm run docker:up

# Production
docker-compose -f infrastructure/docker/docker-compose.prod.yml up -d
```

### Monitoring
- **Logs**: `docker-compose logs -f [service]`
- **Health**: Check `/health` endpoints
- **Metrics**: Prometheus dashboard
- **Errors**: Sentry alerts

### Troubleshooting

#### High Response Times
1. Check Redis cache hit rates
2. Monitor Pinecone query latency
3. Verify LLM API response times
4. Check database connection pools

#### Memory Issues
1. Monitor container memory usage
2. Check for memory leaks in logs
3. Restart services if needed
4. Scale horizontally

#### Database Issues
1. Check MongoDB connection
2. Verify Redis connectivity
3. Monitor Pinecone API limits
4. Check Elasticsearch cluster health

### Maintenance
- **Backups**: MongoDB and Redis backups
- **Updates**: Rolling updates with zero downtime
- **Scaling**: Horizontal scaling based on metrics
- **Monitoring**: 24/7 system monitoring

### Emergency Procedures
- **Rollback**: Use previous Docker image
- **Scale Down**: Reduce replicas during issues
- **Maintenance Mode**: Disable new conversations
- **Data Recovery**: Restore from backups
