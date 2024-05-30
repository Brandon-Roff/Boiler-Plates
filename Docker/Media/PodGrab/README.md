# PodGrab 🎧

PodGrab is a versatile podcast downloader designed to simplify the process of managing and organizing your favorite podcasts. With PodGrab, you can automatically download new episodes of your subscribed podcasts, ensuring you never miss an update from your favorite shows.

## 🌟 Features

- **Podcast Subscription Management**: PodGrab allows you to subscribe to your favorite podcasts and automatically downloads new episodes as they become available.
- **Automatic Download**: Once subscribed, PodGrab automatically fetches new episodes, saving you time and effort.
- **Customizable Download Options**: You can customize download settings such as download schedule, download location, and episode retention policies to suit your preferences.
- **Episode Organization**: PodGrab helps you keep your podcast library organized by sorting episodes into folders based on podcast name, release date, or any other criteria you define.
- **Offline Listening**: Downloaded episodes are stored locally, allowing you to listen offline whenever and wherever you want.
- **Podcast Discovery**: Discover new podcasts based on your interests using PodGrab's built-in podcast directory or by importing podcast feeds.

## 🚀 Getting Started

To get started with PodGrab, you can follow the installation instructions below. Once installed, you can access the PodGrab interface by opening your browser and navigating to `http://localhost:8787`.



## 🐳 Docker Install

If you prefer to use Docker for installation, you can utilize the provided Docker template:

```bash
sudo mkdir -p /srv/Media/PodGrab/data 

cd /srv/Media/PodGrab

wget https://raw.githubusercontent.com/Brandon-Roff/Boiler-Plates/main/Docker/Media/PodGrab/docker-compose.yml
```

After downloading the Docker Compose file, you can configure it according to your preferences:

```yaml
version: "2.1"
services:
  podgrab:
    image: akhilrex/podgrab:latest
    container_name: Podcasts
    environment:
      - CHECK_FREQUENCY=240
#      - PASSWORD=$PASSWORD   ## Uncomment to enable basic authentication, username = podgrab
      - PGID=123 #Specify Group ID
      - PUID=456 # Specify UID
    volumes:
      - ./data:/config
      - ./Podcasts:/assets #Change Left Location to your podcast location
    ports:
      - 8787:8080
    restart: unless-stopped
```

Remember to adjust the values to match your system configuration. Once configured, you can start the PodGrab container:

```bash
sudo docker-compose up -d 
````

Ensure that the necessary ports are open:

```bash
 ufw allow 8787/tcp
 ```