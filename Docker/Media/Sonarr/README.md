# Sonarr 📺

Sonarr is a PVR (Personal Video Recorder) for Usenet and BitTorrent users. It allows you to automatically download and organize your favorite TV shows, making it easy to keep up with your favorite series.

## 🌟 Features

- **Automatic Episode Downloads**: Sonarr can monitor your favorite TV shows and automatically download new episodes as they become available.
- **Quality Management**: You can set preferred quality profiles to ensure that you always get the best version of your TV shows.
- **Series Management**: Sonarr keeps track of your TV show library, allowing you to easily browse and search for episodes.
- **Calendar View**: The built-in calendar view helps you keep track of upcoming episodes and season premieres.
- **Notifications**: Sonarr can send notifications when new episodes are downloaded or when there are issues with your downloads.

## 🚀 Getting Started

To get started with Sonarr, you can follow the installation instructions in the [official Sonarr documentation](https://sonarr.tv/#downloads). Once installed, you can access the Sonarr web interface by opening your browser and navigating to `http://localhost:8989`.

## 📚 Documentation

For more information on how to use Sonarr and its advanced features, you can refer to the [official Sonarr documentation](https://github.com/Sonarr/Sonarr/wiki)

## 🐳 Docker Install

If you would like to install this via docker I have a [template](https://github.com/Brandon-Roff/Boiler-Plates/blob/main/Docker/Media/Sonarr/docker-compose.yml) you can use that includes Permissions and healthcheck

or to download do the following 

```bash
sudo mkdir -p /srv/Media/Sonarr/data 

cd /srv/Media/Sonarr

wget https://raw.githubusercontent.com/Brandon-Roff/Boiler-Plates/main/Docker/Media/Sonarr/docker-compose.yml
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
        image: ghcr.io/linuxserver/sonarr:latest
        restart: always
        volumes:
            - './config:/config' # Point to config folder you may want a volume 
            - '/Videos/TV-Shows:/tv' # Point to your Shows or media
            - '/Downloads:/downloads' # Point to your Downloads
            - '/Archive/Backup:/backup' # Point to your backup/Archive
        environment:
            - TZ=Europe/London #Set you TZ
            - PGID=123 #your UUID
            - PUID=254 #your GUID
        ports:
            - '8989:8989' #Change Left for host port change
        container_name: Sonarr_TV # Docker Container Name
        hostname: Sonarr_TV # Docker Hostname
        healthcheck: # Docker Health check
          test: ["CMD", "wget", "--quiet", "--tries=1", "--spider", "http://localhost:8989/health"]
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


## 🤝 Contributing

If you would like to contribute to Sonarr, please check out the [contribution guidelines](https://github.com/Sonarr/Sonarr/blob/develop/.github/CONTRIBUTING.md).

## 📃 License

Sonarr is released under the [GPLv3 license](https://github.com/Sonarr/Sonarr/blob/develop/LICENSE.md).