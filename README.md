RESTREAMER
==========

This docker container does the following

1. Start nginx with RTMP module that restream to many RTMP servers including Facebook with stunnel
1. Runs stunnel with facebook live server tunneling configuration
1. Reads SRTMP push servers from the environment variables so no need to change nginx configuration
1. Uses RTMP application name from environment variables so you can change it easily to some long random token

## Setup

1. Copy `.env.sample` content to `.env` on your machine
1. Change values in `.env` to set your secret token
1. PLATFORMS environment variable is a comma separated names of other environment variables that hold the RTMP values
1. to stream to FACEBOOK use `rtmp://127.0.0.1:1936/rtmp/` instead of `rtmps://live-api-s.facebook.com:443/rtmp/`

## STREAMING URLS Pages

1. Facebook: `https://www.facebook.com/live/producer/`
1. Youtube: `https://www.youtube.com/live_dashboard`
1. Twitch `https://dashboard.twitch.tv/u/internalerr/settings/channel` servers list `https://stream.twitch.tv/ingests/`
1. Mixer `https://mixer.com/dashboard/channel/broadcast` servers list `https://watchbeam.zendesk.com/hc/en-us/articles/209659883-How-to-Change-Your-Ingest-Server`


## Starting from source

```
docker build . -t restreamer
docker stop restreamer
docker rm restreamer
docker run -d -p 1935:1935 --env-file .env --name restreamer restreamer
```

## OBS config

1. stream server url `rtmp://127.0.0.1/<TOKEN VALUE>`

# CONSTRIBUTORS

Most of the dockerfile code is from https://github.com/tiangolo/nginx-rtmp-docker so many thanks for him
