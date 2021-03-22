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

1. LIVE
2. RELIVE
3. ARCHIVE
4. EXPIRING
5. AWAITING_PUSH

## Storage-id

Storage id should be a way for the system to identify where the video is saved.  
For stage 1 & 2 this should just be the video id  
For stage 3 this should be the archive id  
For stage 4 this should be the sia-sky uri  
For stage 5 this should just be the archive id.

## Moderation-flags

Flags regarding penalties and boosts detailed in [Multipliers](recommendations/multipliers.md)
Flags:

1. Early warning penalty
2. Guidelines violation
3. Unsure community violation
4. NSFW content penalty
5. Early creator boost

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
Please note that all videos in this state is also in the RELIVE state.

## RELIVE

### Criteria

- Watched a bit, not trending
- Videos in the golden period of recommended multipliers

### What this state does

The video should be stored in a folder with the video id as the file name.

## ARCHIVE

### Criteria

- Not usually watched
- Videos on their way out of the golden period

### What this state does

The video will be collected into collections of gzipped files and stored on our servers.  
The target is to keep the total size of collections under 50 gigs.

## EXPIRING

### Criteria

- Basically never watched videos
- We are out of space in the archive

### What this state does

The collection will be uploaded to sia.tech using [Sia Skynet](https://skynet.net)  
The data will be deleted after 30d so after 15d the archive will be sent to all creators which have a video in the
collection. If they log on when the videos are in the AWAITING_PUSH state, it will be republished to Skynet by the user
then updated on the database index.

## AWAITING_PUSH

### Criteria

- The 30d EXPIRING time has expired.

### What this state does

Any videos in this state will be unavailable.  
When any client logs on it will check if any videos it has stored is in this state, it will upload it to Skynet and send
back the url