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
  "public": true,
  "like-count": 0,
  "liked-by": [
    "024e78c5-27a0-4d0f-95c7-4b7a3d952067"
  ],
  "storage-stage": 0,
  "storage-id": "024e78c5-27a0-4d0f-95c7-4b7a3d952067",
  "moderation-flags": 0,
  "flags": 0
}
```

## Id

The id should be a UUID

## Creator

Creator should be a foreign key to link to the creator.

## Public

Whether the user set the video to public or not.

## Like count

Like count should essentially just be the size of liked-by, just to optimise speed

## Liked-by

Liked by should be a many-to-one relation with the creator id as the foreign key

## Storage-stage

Storage stage should be an int detailing which stage its stored in

0. LIVE
1. RELIVE
2. ARCHIVE
3. EXPIRING
4. AWAITING_PUSH

## Storage-id

Storage id should be a way for the system to identify where the video is saved.  
For stage 0 & 1 this should just be the video id  
For stage 2 this should be the archive id  
For stage 3 this should be the sia-sky uri  
For stage 4 this should just be null.

## Moderation-flags

Flags regarding penalties and boosts detailed in [Multipliers](recommendations/multipliers.md)
Flags:

1. Early warning penalty
2. Guidelines violation
3. NSFW content penalty
4. Early creator boost

## Flags

General flags regarding things like force_private Flags:

1. Force private
2. No penalties
3. NSFW content
4. Flashing content

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

This state will store the information in the cache  
Data in this state should have an expiry time of 10 minutes

## RELIVE

### Criteria

- Watched a bit, not trending
- Videos in the golden period of recommended multipliers

### What this state does

The video should be stored in a folder with the video id as the file name.