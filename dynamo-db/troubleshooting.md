## DynamoDB Troubleshooting


TTL didn't delete the items:
https://aws.amazon.com/premiumsupport/knowledge-center/dynamodb-ttl-items-not-deleted/

Resolution:
If you enable TTL on a DynamoDB table, but DynamoDB doesn’t delete the items when they expire, confirm the following:


- Be sure that you set a TTL attribute. For more information, see Enabling Time to Live (TTL).
- TTL attributes must use the number data type. Other data types, such as string, aren't supported.
- TTL attributes must use the epoch time format. For example, the epoch timestamp for May 5, 2020 16:52:32 UTC is 1588697552. You can use a free online converter, such as EpochConverter, to get the correct value.
Note: Be sure that the timestamp is in seconds, not milliseconds (for example, use 1572268323 instead of 1572268323000).
- **Wait at least for 48 hours for DynamoDB to delete the item. DynamoDB deletes expired items on a best-effort basis to be sure that there's enough throughput for other data operations. Processing takes place automatically, in the background, and doesn't affect read or write traffic to the table.**
- Be sure that the expiration date isn't more than five years in the past. DynamoDB doesn't delete items with expiration dates more than five years in the past.


---
