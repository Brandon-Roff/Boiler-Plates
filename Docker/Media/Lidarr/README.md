<p align="center"> <img src="/Images/Media/Lidarr.png" alt="Lidarr Icon" style="width: 25%;"></p>


# Lidarr 🎵

Lidarr is a music collection management tool for Usenet and BitTorrent users. It allows you to automatically download and organize music files, making it easy to enjoy your favorite music with accurate metadata.

## 🌟 Features

- **Automatic Music Downloads**: Lidarr can monitor your music library and automatically download new music releases.
- **Music Collection Management**: You can easily search for and manage your music collection, including album artwork, artist information, and track details.
- **Music Customization**: Lidarr allows you to customize music settings, such as preferred music quality, file formats, and metadata sources.
- **Integration with Media Servers**: Lidarr integrates with popular media servers like Plex, Emby, and Jellyfin to ensure that your music is available for streaming.
- **Notifications**: Lidarr can send notifications when new music releases are downloaded or when there are issues with music downloads.

## 🚀 Getting Started

To get started with Lidarr, you can follow the installation instructions in the [official Lidarr documentation](https://lidarr.audio/#downloads). Once installed, you can access the Lidarr web interface by opening your browser and navigating to `http://localhost:8686`.

## 📚 Documentation

For more information on how to use Lidarr and its advanced features, you can refer to the [official Lidarr documentation](https://github.com/lidarr/Lidarr/wiki)

## 🐳 Docker Install

If you would like to install this via docker I have a [template](https://github.com/Brandon-Roff/Boiler-Plates/blob/main/Docker/Media/Lidarr/docker-compose.yml) you can use that includes Permissions and healthcheck

or to download do the following 

```bash
sudo mkdir -p /srv/Media/Lidarr/data 

cd /srv/Media/Lidarr

wget https://raw.githubusercontent.com/Brandon-Roff/Boiler-Plates/main/Docker/Media/Lidarr/docker-compose.yml
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
        image: lscr.io/linuxserver/Lidarr:latest
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
        container_name: Lidarr_Subtitles # Docker Container Name
        hostname: Lidarr_Subtitles # Docker Hostname
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
sudo ufw allow 8686/tcp
```

## 🤝 Contributing

If you would like to contribute to Lidarr, please check out the [contribution guidelines](https://github.com/lidarr/Lidarr/blob/develop/.github/CONTRIBUTING.md).

## 📃 License

Lidarr is released under the [GPLv3 license](https://github.com/lidarr/Lidarr/blob/develop/LICENSE.md).
