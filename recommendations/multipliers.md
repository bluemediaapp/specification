# The recommendation multipliers

Note: this is only for videos.

Multipliers are made to optimise cost, reduce bad content being seen and keep the site speedy

Cost will be optimised by reducing the views for videos in the ARCHIVE & EXPIRING states as those require more time to
load into the cache and takes longer to be able to display for the end user.

Bad content will be seen by fewer people by only showing to a few people in the start making reporting more effective.

The site will be more speedy because the higher the storage type id, the longer it will take to get the video

# How it works

The multiplier starts at 1x  
Please note that we should notify the user which restrictions have been applied.

# Appealing

Most penalties should be able to be appealed.   
If the appeal is accepted the creator should be notified, and the video should be automatically re-uploaded with a flag
to block all penalties.

## Early penalty

The early penalty is there to protect against explicit content not recognised by our automated systems  
The penalty will be applied to videos uploaded in the last x hours The penalty will be -0.5  
This penalty cannot be appealed, although it will be removed if the video has the no penalties flag

## Early warning penalty

If during the Early penalty stage, the video gets a high report percentage, the video will be added to the reports queue
and given a "Potentially sensitive content" warning before watching  
The video will also be given a -0.90 permanent penalty  
Videos will not be shown to people with the "Show potentially sensitive content" content preference turned off.  
This penalty will not be stacked.

## Guidelines violation penalty

If the video has been voted out by the community, the video will be forced to private.  
If the community are unsure, the video will be given a -0.7 penalty and be sent to the supreme community moderators  
A community notice will be applied to the creator profile, and a high priority notification will be sent

## NSFW content penalty

As much as I want all content to be accepted on my platform, I still want my platform to not become a NSFW sharing
site.  
NSFW content will not be sent to people with the "Show NSFW content" content preference turned off. A small penalty of
-0.2 will be applied to reduce the amount of NSFW content

## Early creator boost

We want to give a welcome our new creators to our platform.  
If there's no other accounts logged in on the device you created it on AND no accounts created on the same IP this will
be applied  
In the 10 first videos uploaded, a +0.1 boost will be applied
