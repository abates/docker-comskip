# Comskip, Dockerized and on Alpine

Runs on Alpine linux (103MB total size) and includes the latest comskip from github.com.  
Also includes ekim1337's python script that runs comskip, removes the found commercials from the video, and finally replaces the original video with the commercial-less video file.

```shell
docker run --rm -d \
    -e TZ="America/New_York" \
    -v /tmp/comskip:/tmp \
    -v /home/user/videos/recordings/:/data \
    djaydev/comskip \
    "/data/recorded-video-file.ts"
```

Where:

- `--rm`: Removes the container once finished. Optional.
- `TZ`: Your timezone
- `/tmp/comskip`: Temp folder for transcoding. This should be local, fast, and have enough free space for ~2x your largest video.  
- `/home/user/videos/recordings/`: The folder where the recording with comercials are saved.
- `/data/recorded-video-file.ts`: The actual file that needs commercials removed. Prefix "/data/" in front of the file name.

The docker image can also be used as a post processing script.  
Example of a post processing script to run on docker host:

```shell
#!/bin/bash
DOCKER=/usr/bin/docker

${DOCKER} run --rm -v "/tmp/comskip:/tmp" -v "$1:/data$1" djaydev/comskip "/data$1"
```

## Credits

Python script from:             www.github.com/ekim1337/PlexComskip  
Comskip program itself:         www.github.com/erikkaashoek/Comskip  
Comskip.ini settings file from: www.github.com/plexinc/pms-docker
