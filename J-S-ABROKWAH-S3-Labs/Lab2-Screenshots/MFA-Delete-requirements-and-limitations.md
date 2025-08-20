# Lab 2: MFA Delete Requirements and Limitations

## MFA Delete Configuration Requirements

### Prerequisites
- **Root user access required** - Only the AWS account root user can enable/disable MFA Delete
- **AWS CLI installed and configured** with root user credentials
- **MFA device configured** - Virtual or hardware MFA device associated with root user

### Configuration Command Structure
```bash
aws s3api put-bucket-versioning \
  --bucket [YOUR-BUCKET-NAME] \
  --versioning-configuration Status=Enabled,MFADelete=Enabled \
  --mfa "arn:aws:iam::[ACCOUNT-ID]:mfa/[MFA-DEVICE-NAME] [MFA-CODE]"
```

## MFA Delete Behavior

### When MFA Delete is Enabled
MFA token is **required** for:
- **Permanently deleting object versions**
- **Suspending versioning on the bucket**

### When MFA Delete is NOT Required
- **Regular delete operations** (still create delete markers)
- **Uploading new object versions**
- **Restoring objects by deleting delete markers**

## Limitations and Considerations

### Access Limitations
- **Console limitation**: Cannot enable MFA Delete through AWS Console
- **IAM user limitation**: IAM users cannot enable MFA Delete, even with full S3 permissions
- **API/CLI only**: Must use AWS CLI or API calls

### Security Benefits
- **Enhanced protection**: Prevents accidental permanent deletion of critical data
- **Compliance requirement**: Meets regulatory requirements for data retention
- **Audit trail**: All MFA Delete operations are logged in CloudTrail

### Operational Impact
- **Increased complexity**: Requires MFA token for certain operations
- **Root user dependency**: Creates operational dependency on root user access
- **Emergency access**: Consider emergency procedures for MFA device loss

## Best Practices
- **Enable for critical buckets** containing irreplaceable data
- **Document procedures** for MFA Delete operations
- **Test recovery scenarios** before implementing in production
- **Consider alternative approaches** like bucket policies for less critical data