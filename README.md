# media-services

```yaml
name: media-services
services:
  prowlarr:
    image: lscr.io/linuxserver/prowlarr:latest
    container_name: prowlarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=America/Sao_Paulo
    volumes:
      - D:/prowlarr/config:/config
    ports:
      - 9696:9696
    networks:
      - media
    restart: unless-stopped

  radarr:
    image: lscr.io/linuxserver/radarr:latest
    container_name: radarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=America/Sao_Paulo
    volumes:
      - D:/radarr/config:/config
      - D:/radarr/movies:/movies
      - D:/downloads:/downloads
    ports:
      - 7878:7878
    networks:
    - media
    restart: unless-stopped

  sonarr:
    image: lscr.io/linuxserver/sonarr:latest
    container_name: sonarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=America/Sao_Paulo
    volumes:
        - D:/sonarr/config:/config
        - D:/sonarr/tv:/tv
        - D:/downloads:/downloads
    ports:
      - 8989:8989
    networks:
      - media
    restart: unless-stopped

  flaresolverr:
    image: ghcr.io/flaresolverr/flaresolverr:latest
    container_name: flaresolverr
    environment:
      - LOG_LEVEL=info
      - TZ=America/Sao_Paulo
    ports:
      - 8191:8191
    networks:
      - media
    restart: unless-stopped

networks:
  media:
    driver: bridge
```
