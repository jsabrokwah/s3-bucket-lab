# Lab 1: Storage Classes Cost Comparison

## AWS S3 Storage Classes - Cost Analysis

### Storage Costs (per GB per month)

| Storage Class | Cost per GB/month | Use Case |
|---------------|-------------------|----------|
| **Standard** | $0.023 | Frequently accessed data |
| **Standard-IA** | $0.0125 + retrieval costs | Infrequently accessed data |
| **Intelligent-Tiering** | $0.023 + monitoring costs | Unknown access patterns |

### Key Cost Considerations

#### Standard Storage Class
- **Cost**: $0.023/GB/month
- **Best for**: Frequently accessed data
- **No retrieval fees**
- **No minimum storage duration**

#### Standard-IA (Infrequent Access)
- **Cost**: $0.0125/GB/month
- **Additional costs**: Retrieval fees apply
- **Minimum storage duration**: 30 days
- **Best for**: Data accessed less than once per month

#### Intelligent-Tiering
- **Cost**: $0.023/GB/month + $0.0025 per 1,000 objects monitored
- **Automatic optimization**: Moves objects between access tiers
- **Best for**: Unknown or changing access patterns
- **No retrieval fees** for automatic transitions

### Cost Optimization Strategy
For 1GB stored for 1 month:
- **Standard**: $0.023
- **Standard-IA**: $0.0125 (if no retrievals)
- **Intelligent-Tiering**: $0.023 + monitoring fees

**Recommendation**: Use Standard-IA for data accessed less than monthly, Intelligent-Tiering for unpredictable patterns.