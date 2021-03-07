# nginx-rtmp

[**Docker**](https://www.docker.com/) image with [**Nginx**](http://nginx.org/en/) using the [**nginx-rtmp-module**](https://github.com/arut/nginx-rtmp-module) module for live multimedia (video) streaming.

## Description

This [**Docker**](https://www.docker.com/) image can be used to create an RTMP server for multimedia / video streaming using [**Nginx**](http://nginx.org/en/) and [**nginx-rtmp-module**](https://github.com/arut/nginx-rtmp-module), built from the current latest sources (Nginx 1.19.6 and nginx-rtmp-module 1.2.1).

This was inspired by other similar previous images from [Tiangolo](https://github.com/tiangolo/nginx-rtmp-docker) and by an [OBS Studio post](https://obsproject.com/forum/resources/how-to-set-up-your-own-private-rtmp-server-using-nginx.50/).

The main purpose (and test case) to build it was to allow streaming from [**OBS Studio**](https://obsproject.com/) to different clients at the same time.

**GitHub repo**: <https://github.com/hrmuwanika/nginx-rtmp-docker>

## Details

## How to use
* Build and run the container 
 
 ```bash
 git clone  https://github.com/hrmuwanika/nginx-rtmp-docker
 cd nginx-rtmp-docker
 docker build -t hrmuwanika/nginx_rtmp .
 docker images
 ```
 
* For the simplest case, just run a container with this image:
 
```bash
docker run -d -p 1935:1935 -p 8080:8080 --name nginx-rtmp hrmuwanika/nginx_rtmp
```

## How to test with OBS Studio and VLC

* Run a container with the command above


* Open [OBS Studio](https://obsproject.com/)
* Click the "Settings" button
* Go to the "Stream" section
* In "Stream Type" select "Custom Streaming Server"
* In the "URL" enter the `rtmp://<ip_of_host>:1935/live` replacing `<ip_of_host>` with the IP of the host in which the container is running. For example: `rtmp://45.99.213.78:1935/live`
* In the "Stream key" use a "key" that will be used later in the client URL to display that specific stream. For example: `stream_name`
* Click the "OK" button
* In the section "Sources" click de "Add" button (`+`) and select a source (for example "Screen Capture") and configure it as you need
* Click the "Start Streaming" button


* Open a [VLC](http://www.videolan.org/vlc/index.html) player (it also works in Raspberry Pi using `omxplayer`)
* Click in the "Media" menu
* Click in "Open Network Stream"
* Enter the URL from above as `http://<ip_of_host>:8080/hls/stream_name/index.m3u8` or `http://<ip_of_host>:8080/dash/stream_name/index.mpd`replacing `<ip_of_host>` with the IP of the host in which the container is running and `<key>` with the key you created in OBS Studio. For example: `http://45.99.213.78:8080/hls/stream_name/index.m3u8` http://45.99.213.78:8080/dash/stream_name/index.mpd`
* Click "Play"
* Now VLC should start playing whatever you are transmitting from OBS Studio

