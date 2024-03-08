<p align="center"> <img src="/Images/Media/Prowlarr.png" alt="Prowlarr Icon"></p>


# Prowlarr 📺

Prowlarr is an indexer specifically designed for Usenet and BitTorrent users. It serves as a tool that helps you automatically download and organize your favorite TV shows, making it convenient to keep up with your preferred series. Essentially, Prowlarr simplifies the process of finding and managing TV show content from Usenet and BitTorrent sources.

## 🌟 Features

- **Indexer for Usenet and BitTorrent**: Prowlarr is specifically designed for Usenet and BitTorrent users, providing a comprehensive indexing solution.
- **Automatic Content Download**: Prowlarr can automatically download your favorite TV shows as soon as they become available, saving you time and effort.
- **Quality Management**: You can set preferred quality profiles to ensure that you always get the best version of your TV shows.
- **Series Management**: Prowlarr keeps track of your TV show library, making it easy to browse and search for episodes.
- **Calendar View**: The built-in calendar view helps you stay organized by displaying upcoming episodes and season premieres.
- **Notifications**: Prowlarr can send notifications when new episodes are downloaded or when there are issues with your downloads.

## 🚀 Getting Started

To get started with Prowlarr, you can follow the installation instructions in the [official Prowlarr documentation](https://prowlarr.com/#downloads). Once installed, you can access the Prowlarr web interface by opening your browser and navigating to `http://localhost:9696`.

## 📚 Documentation

For more information on how to use Prowlarr and its advanced features, you can refer to the [official Prowlarr documentation](https://github.com/Prowlarr/Prowlarr/wiki)

## 🐳 Docker Install

If you would like to install this via docker I have a [template](https://github.com/Brandon-Roff/Boiler-Plates/blob/main/Docker/Media/Prowlarr/docker-compose.yml) you can use that includes Permissions and healthcheck

or to download do the following 

```bash
sudo mkdir -p /srv/Media/Prowlarr/data 

cd /srv/Media/Prowlarr

wget https://raw.githubusercontent.com/Brandon-Roff/Boiler-Plates/main/Docker/Media/Prowlarr/docker-compose.yml
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
        image: lscr.io/linuxserver/prowlarr:latest
        restart: always
        volumes:
            - './config:/config' # Point to config folder you may want a volume 
            - '/Archive/Backup:/backup' # Point to your backup/Archive
        environment:
            - TZ=Europe/London #Set you TZ
            - PGID=123 #your UUID
            - PUID=254 #your GUID
        ports:
            - '9696:9696' # Change Left for host port change
        container_name: Prowlarr_Indexers # Docker Container Name
        hostname: Prowlarr_Indexers # Docker Hostname
        healthcheck: # Docker Health check
          test: ["CMD", "wget", "--quiet", "--tries=1", "--spider", "http://localhost:9696/health"]
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
sudo ufw allow 9696/tcp
```

## 🤝 Contributing

If you would like to contribute to Prowlarr, please check out the [contribution guidelines](https://github.com/Prowlarr/Prowlarr/blob/develop/.github/CONTRIBUTING.md).

## 📃 License

Prowlarr is released under the [GPLv3 license](https://github.com/Prowlarr/Prowlarr/blob/develop/LICENSE.md).