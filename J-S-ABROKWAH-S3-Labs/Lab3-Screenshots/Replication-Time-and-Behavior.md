# Lab 3: Cross-Region Replication - Timing and Behavior Analysis

## Replication Timing Observations

### Initial Replication
- **Average time**: 1-2 minutes for small files (<1MB)
- **Factors affecting timing**:
  - File size
  - Network conditions
  - AWS service load
  - Source and destination regions

### Replication Monitoring
- **Replication metrics enabled** in configuration
- **CloudWatch metrics** available for monitoring replication status
- **Replication status** visible in object properties

## Replication Behavior Differences

### Object Replication
| Operation | Source Bucket | Destination Bucket | Notes |
|-----------|---------------|-------------------|-------|
| **New object upload** | Object created | Object replicated | Storage class changed to Standard-IA |
| **Object modification** | New version created | New version replicated | Version IDs differ between buckets |
| **Object deletion** | Delete marker created | **No replication** | Delete markers not replicated by default |

### Version Management
- **Version IDs**: Different between source and destination
- **Metadata preservation**: All metadata replicated
- **Storage class**: Changed to Standard-IA as configured
- **Timestamps**: Replication timestamp differs from original

### Delete Behavior Analysis
1. **Standard delete** on source creates delete marker
2. **Delete marker NOT replicated** to destination (default behavior)
3. **Object remains accessible** in destination bucket
4. **Permanent deletion** requires explicit version deletion

## Key Findings

### What Replicates
✅ New object uploads  
✅ Object modifications (new versions)  
✅ Object metadata  
✅ Object tags  

### What Does NOT Replicate
❌ Delete markers (by default)  
❌ Objects uploaded before replication rule  
❌ Objects in Glacier or Glacier Deep Archive  
❌ Server-side encryption with customer-provided keys  

## Real-World Implications

### Disaster Recovery
- **Data availability**: Objects remain accessible in destination region
- **Version consistency**: All versions replicated for complete history
- **Delete protection**: Accidental deletions don't affect destination

### Compliance Considerations
- **Data residency**: Objects stored in multiple regions
- **Retention policies**: May need separate lifecycle rules per region
- **Cost implications**: Storage costs in multiple regions

### Operational Notes
- **Monitoring required**: Set up CloudWatch alarms for replication failures
- **Testing recommended**: Regular testing of replication functionality
- **Documentation critical**: Clear procedures for failover scenarios