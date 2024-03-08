<p align="center"> <img src="/Images/Media/Radarr.png" alt="Sonarr Icon"></p>


# Radarr 🎥

Radarr is a movie collection manager for Usenet and BitTorrent users. It allows you to automatically download and organize your favorite movies, making it easy to keep up with your movie collection.

## 🌟 Features

- **Automatic Movie Downloads**: Radarr can monitor your favorite movies and automatically download new releases as they become available.
- **Quality Management**: You can set preferred quality profiles to ensure that you always get the best version of your movies.
- **Collection Management**: Radarr keeps track of your movie library, allowing you to easily browse and search for movies.
- **Calendar View**: The built-in calendar view helps you keep track of upcoming movie releases.
- **Notifications**: Radarr can send notifications when new movies are downloaded or when there are issues with your downloads.

## 🚀 Getting Started

To get started with Radarr, you can follow the installation instructions in the [official Radarr documentation](https://radarr.video/#downloads). Once installed, you can access the Radarr web interface by opening your browser and navigating to `http://localhost:7878`.

## 📚 Documentation

For more information on how to use Radarr and its advanced features, you can refer to the [official Radarr documentation](https://github.com/Radarr/Radarr/wiki)

## 🐳 Docker Install

If you would like to install this via docker I have a [template](https://github.com/Brandon-Roff/Boiler-Plates/blob/main/Docker/Media/Radarr/docker-compose.yml) you can use that includes Permissions and healthcheck

or to download do the following 

```bash
sudo mkdir -p /srv/Media/Radarr/data 

cd /srv/Media/Radarr

wget https://raw.githubusercontent.com/Brandon-Roff/Boiler-Plates/main/Docker/Media/Radarr/docker-compose.yml
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
        image: lscr.io/linuxserver/radarr:latest
        restart: always
        volumes:
            - './data:/config' # Point to config folder you may want a volume 
            - '/Videos/Movies:/Movies' # Point to your Films or media
            - '/Downloads:/downloads' # Point to your Downloads
            - '/Archive/Backup:/backup' # Point to your backup/Archive
        environment:
            - TZ=Europe/London #Set you TZ
            - PGID=123 #your UUID
            - PUID=254 #your GUID
        ports:
            - '7878:7878' # Change Left for host port change
        container_name: Radarr_Movies # Docker Container Name
        hostname: Radarr_Movies # Docker Hostname
        healthcheck: # Docker Health check
          test: ["CMD", "wget", "--quiet", "--tries=1", "--spider", "http://localhost:7878/health"]
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
sudo ufw allow 7878/tcp
```

## 🤝 Contributing

If you would like to contribute to Radarr, please check out the [contribution guidelines](https://github.com/Radarr/Radarr/blob/develop/.github/CONTRIBUTING.md).

## 📃 License

Radarr is released under the [GPLv3 license](https://github.com/Radarr/Radarr/blob/develop/LICENSE.md).
