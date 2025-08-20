# AWS S3 Labs - Comprehensive Lab Report
**Student**: J.S. Abrokwah  
**Date**: [Lab Completion Date]  
**Course**: DevOps Training - Solutions Architect Associate Preparation

---

## Lab 1: Storage Classes & Lifecycle Policies

### What Worked as Expected
- **Bucket creation** with unique naming convention successful
- **Storage class assignment** during upload worked correctly
- **Lifecycle rule creation** with multiple transitions configured properly
- **Cost calculator** provided clear pricing comparisons

### Challenges Encountered
- Actually, no challenges were encounted as expected.

### Real-World Application
- **Automated cost optimization** for long-term data storage
- **Compliance requirements** for data retention periods
- **Archive strategies** for backup and disaster recovery data
- **Media companies** could use for video content lifecycle management

### Cost Implications Observed
- **Standard-IA savings**: 46% cost reduction for infrequently accessed data
- **Glacier transitions**: Significant savings for long-term archival
- **Intelligent-Tiering**: Best for unpredictable access patterns despite monitoring costs

---

## Lab 2: Versioning & MFA Delete

### What Worked as Expected
- **Versioning enablement** during bucket creation
- **Multiple versions** created and managed successfully
- **Delete marker behavior** functioned as documented
- **Object restoration** by removing delete markers

### Challenges Encountered
- **MFA Delete limitation** - requires root user and CLI access
- **Version management complexity** - understanding version IDs
- **Storage cost implications** - multiple versions increase costs

### Real-World Application
- **Document management systems** requiring version history
- **Compliance environments** needing audit trails
- **Development workflows** for code and configuration management
- **Financial institutions** requiring data immutability

### Key Insights
- **Versioning protection** prevents accidental data loss
- **MFA Delete security** provides additional protection layer
- **Operational complexity** increases with versioning enabled
- **Cost monitoring** essential with multiple versions

---

## Lab 3: Cross-Region Replication (CRR)

### What Worked as Expected
- **Bucket creation** in different regions successful
- **IAM role configuration** for replication permissions
- **Replication rule setup** with storage class changes
- **Object replication** occurred within expected timeframe

### Challenges Encountered
- **IAM permissions complexity** - ensuring proper role configuration
- **Replication timing** - 2-3 minute delay for small files
- **Delete behavior understanding** - delete markers not replicated by default

### Real-World Application
- **Disaster recovery strategies** for critical business data
- **Global content distribution** for multinational organizations
- **Compliance requirements** for data residency in multiple regions
- **Backup strategies** with geographic separation

### Replication Behavior Observations
- **Automatic replication** of new objects and versions
- **Metadata preservation** across regions
- **Storage class transformation** during replication
- **Delete protection** - objects remain in destination despite source deletion

---

## Overall Learning Outcomes

### Technical Skills Developed
- **S3 bucket management** and configuration
- **IAM role creation** and permission management
- **Lifecycle policy design** for cost optimization
- **Cross-region replication** setup and monitoring

### AWS Services Integration
- **S3 and IAM** integration for secure access
- **CloudWatch** for monitoring and metrics
- **AWS CLI** for advanced configurations
- **Cost management** tools and calculators

### Best Practices Learned
- **Naming conventions** for resource organization
- **Security configurations** with MFA and versioning
- **Cost optimization** through storage class selection
- **Disaster recovery** planning with replication

---

## Recommendations for Production Implementation

### Security Considerations
- **Enable MFA Delete** for critical buckets
- **Implement bucket policies** for access control
- **Use IAM roles** instead of user credentials
- **Enable CloudTrail** for audit logging

### Cost Optimization
- **Implement lifecycle policies** for all buckets
- **Monitor storage class usage** regularly
- **Use Intelligent-Tiering** for unknown access patterns
- **Set up billing alerts** for cost monitoring

### Operational Excellence
- **Document all configurations** and procedures
- **Test disaster recovery** scenarios regularly
- **Monitor replication status** with CloudWatch
- **Implement automated cleanup** procedures

---

## Assessment Question Responses

### Lab 1 Assessment
1. **Cost impact of Standard to Standard-IA**: Approximately 46% cost reduction, but adds retrieval costs and 30-day minimum duration
2. **Direct transition to Glacier Deep Archive**: No, must follow transition hierarchy through intermediate classes
3. **Standard-IA minimum duration**: 30 days - objects deleted before this incur early deletion fees

### Lab 2 Assessment
1. **Previous versions behavior**: Remain intact when new versions uploaded, accessible via version ID
2. **Permanent version deletion**: Select specific version ID and delete, or use MFA Delete if enabled
3. **Root user MFA Delete requirement**: Security measure to prevent unauthorized permanent deletions, only root has this privilege

### Lab 3 Assessment
1. **CRR prerequisites**: Versioning enabled on both buckets, different regions, proper IAM role with replication permissions
2. **Delete marker replication**: No, delete markers are not replicated by default (configurable option)
3. **Same region replication**: No, CRR requires different regions; use Same-Region Replication (SRR) for same region

---

## Cleanup Confirmation
- ✅ All objects deleted from all buckets (including versions)
- ✅ All lifecycle rules removed
- ✅ All replication rules removed
- ✅ All buckets deleted successfully
- ✅ IAM role `lab3-s3-replication-role` deleted
- ✅ No remaining charges in billing dashboard
