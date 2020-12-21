## Notes


### Security 
- You can't convert an unencrypted DB cluster to an encrypted one. However, you can restore an unencrypted snapshot to an encrypted Aurora DB cluster. To do this, specify a CMK when you restore from the unencrypted snapshot.
  - You cannot create an encrypted copy of an unencrypted snapshot. However, this works for Amazon RDS.
  - https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Overview.Encryption.html#Overview.Encryption.Limitations
  
