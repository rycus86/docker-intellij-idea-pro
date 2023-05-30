Docker container to run IntelliJ IDEA Ultimate Edition (https://www.jetbrains.com/idea/)

### Usage

```
docker run --rm \
  -e DISPLAY=${DISPLAY} \
  -v /tmp/.X11-unix:/tmp/.X11-unix \
  -v ~/.Idea:/home/developer/.Idea \
  -v ~/.Idea.java:/home/developer/.java \
  -v ~/.Idea.maven:/home/developer/.m2 \
  -v ~/.Idea.gradle:/home/developer/.gradle \
  -v ~/.Idea.share:/home/developer/.local/share/JetBrains \
  -v ~/Project:/home/developer/Project \
  --name idea-$(head -c 4 /dev/urandom | xxd -p)-$(date +'%Y%m%d-%H%M%S') \
rycus86/intellij-idea-pro:${IDE_VERSION}
```

Docker Hub Page: https://hub.docker.com/r/rycus86/intellij-idea-pro/
([available versions](https://hub.docker.com/r/rycus86/intellij-idea-pro/tags))

### OS X instructions

1. Install XQuartz from https://www.xquartz.org/releases/
2. Configure `Allow connections from network clients` in the settings
    - Restart the system (needed only once when this is enabled)
3. Run `xhost +localhost` in a terminal to allow connecting to X11 over the TCP socket
4. Use `-e DISPLAY=host.docker.internal:0` for passing the `${DISPLAY}` environment

#### For Windows hosts (simplified):

```
docker.exe run --rm -d ^
     --name intellij-idea-pro ^
     -e DISPLAY=YOUR_IP_ADDRESS:0.0 ^
     -v %TEMP%\.X11-unix:/tmp/.X11-unix ^
     -v %USERPROFILE%\intellij-idea:/home/developer ^
     rycus86/intellij-idea-pro:%IDE_VERSION%
```

### Notes

You'll still need a license to use the application!

The IDE will have access to AdoptOpenJDK 8 and to Git as well.
Project folders need to be mounted like `-v ~/Project:/home/developer/Project`.
The actual name can be anything - I used something random to be able to start multiple instances if needed.
You might want to consider using `--network=host` if you're running servers from the IDE.
