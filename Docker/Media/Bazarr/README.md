<p align="center"> <img src="/Images/Media/Bazarr.png" alt="Bazarr Icon"></p>


# Bazarr 🎥

Bazarr is a subtitle management tool for Usenet and BitTorrent users. It allows you to automatically download and organize subtitles for your favorite movies and TV shows, making it easy to enjoy your media with accurate subtitles.

## 🌟 Features

- **Automatic Subtitle Downloads**: Bazarr can monitor your movie and TV show library and automatically download subtitles in your preferred languages.
- **Subtitle Management**: You can easily search for and manage subtitles for your media collection.
- **Subtitle Customization**: Bazarr allows you to customize subtitle settings, such as preferred languages, providers, and quality.
- **Integration with Media Servers**: Bazarr integrates with popular media servers like Plex, Emby, and Jellyfin to ensure that subtitles are available for your media.
- **Notifications**: Bazarr can send notifications when new subtitles are downloaded or when there are issues with subtitle downloads.

## 🚀 Getting Started

To get started with Bazarr, you can follow the installation instructions in the [official Bazarr documentation](https://www.bazarr.media/#downloads). Once installed, you can access the Bazarr web interface by opening your browser and navigating to `http://localhost:6767`.

## 📚 Documentation

For more information on how to use Bazarr and its advanced features, you can refer to the [official Bazarr documentation](https://github.com/morpheus65535/bazarr/wiki)

## 🐳 Docker Install

If you would like to install this via docker I have a [template](https://github.com/Brandon-Roff/Boiler-Plates/blob/main/Docker/Media/Bazarr/docker-compose.yml) you can use that includes Permissions and healthcheck

or to download do the following 

```bash
sudo mkdir -p /srv/Media/Bazarr/data 

cd /srv/Media/Bazarr

wget https://raw.githubusercontent.com/Brandon-Roff/Boiler-Plates/main/Docker/Media/Bazarr/docker-compose.yml
```

then you want to said your vairables

```bash
sudo nano docker-compose.yml
```
or if you use vim

```bash
sudo vim docker-compose.yml
```

The docker compose file will look like below

```yaml
version: '3.9'
services:
    linuxserver:
        image: lscr.io/linuxserver/bazarr:latest
        restart: always
        volumes:
            - './data:/config' # Point to config folder you may want a volume 
            - '/Videos/Movies:/Movies' # Point to your Films or media
            - '/Videos/TV:/TV' # Point to your Downloads
            - '/Archive/Backup:/backup' # Point to your backup/Archive
        environment:
            - TZ=Europe/London #Set you TZ
            - PGID=123 #your UUID
            - PUID=254 #your GUID
        ports:
            - '6767:6767' # Change Left for host port change
        container_name: Bazarr_Subtitles # Docker Container Name
        hostname: Bazarr_Subtitles # Docker Hostname
        healthcheck: # Docker Health check
          test: ["CMD", "wget", "--quiet", "--tries=1", "--spider", "http://localhost:6767/health"]
          interval: 30s
          timeout: 10s
          retries: 5
```

to find your id/gid of the user use the below command

```bash
id username
```

After changing the values to match your layout you can run the container headless by running  (-d means detached)

```bash
sudo docker-compose up -d 
```

Also remeber to allow port through UFW

```bash
sudo ufw allow 6767/tcp
```

## 🤝 Contributing

If you would like to contribute to Bazarr, please check out the [contribution guidelines](https://github.com/bazarr/bazarr/blob/develop/.github/CONTRIBUTING.md).

## 📃 License

Bazarr is released under the [GPLv3 license](https://github.com/bazarr/bazarr/blob/develop/LICENSE.md).
