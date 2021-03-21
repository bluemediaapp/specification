# General information
Criteria should match one or more of the listed requirements.  
Videos are provided by a "CDN" microservice.

# Compression
All videos should be lossless compressed before being stored on any servers.  
Videos should be compressed before being sent to our servers AND on our servers.

# Indexing
Videos should be indexed in the database in the following schema
```json
{
  "id": "024e78c5-27a0-4d0f-95c7-4b7a3d952067",
  "creator": "c7ea5d40-a8f5-47e9-90ce-abec19d1a1ac",
  "like-count": 0,
  "liked-by": [
    "ddcd4f6b-eb19-47e4-ae1b-863353ba6466"
  ],
  "storage-stage": 0,
  "storage-id": null
}
```

# Storage levels
Storage will be performed in different levels

- LIVE
- RELIVE
- DISK
- ARCHIVE
- EXPIRING
- AWAITING_PUSH


## LIVE
### Criteria:
- Trending
- About to be shown via the 5 videos on each side of the currently playing video in the recommended feed
- Not moved to DISK yet.

### What this state does
This state will store the information in cache
Data in this state should have an expiry time of 10 minutes


## RELIVE
### Criteria
- Watched a bit, not trending
- Videos in the golden period of recommended multipliers

### What this state does
The video should be stored in a folder with the video id as the file name.