# sealedsecrets-s3-backup

## About
This cronjob will save all active SealedSecrets keys to a S3 bucket.

- Get all keys by using label selector `sealedsecrets.bitnami.com/sealed-secrets-key=active`
- Create `tar.gz` archive of extracted `YAML` files
- Upload to given S3 bucket using `curl`

Note: The backup script is very basic and has no built-in error checking

## S3 Lifecycle Policy Example
```json
{
   "Rules":[
      {
         "ID":"rule1",
         "Prefix":"",
         "Expiration":{
            "Days":30
         },
         "Status":"Enabled"
      }
   ]
}
```
```bash
# create lifecycle policy
aws s3api put-bucket-lifecycle-configuration --bucket sealedsecrets --lifecycle-configuration file://bkt-lc-config.kson
```