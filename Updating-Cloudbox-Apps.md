This is particularly useful if you wanted to update a specific app. 

_Note: To update the entire Cloudbox project, see [[Updating Cloudbox]]._


| Cloudbox Apps          | How to update                                                                                  |
|:---------------------- |:---------------------------------------------------------------------------------------------- |
| Plex                   | Restart the docker container: `docker stop plex && docker start plex`                              |
| PlexPy                 | Update within the app.                                                                         | 
| Plex AutoScan          | Update: `cd /opt/plex_autoscan && git pull` <br /> Restart: `sudo systemctl restart plex_autoscan.service`                                        |
| Sonarr                 | Restart the docker container: `docker stop sonarr && docker start sonarr`                          |
| Radarr                 | Restart the docker container: `docker stop radarr && docker start radarr`                          |
| NZBGet                 | Restart the docker container: `docker stop nzbget && docker start nzbget`                          |
| rTorrent               | Update the docker container: `cd ~/cloudbox && sudo ansible-playbook cloudbox.yml --update-rutorrent` |
| Jackett                | Restart the docker container: `docker stop jackett && docker start jackett`                        |
| NZB Hydra              | Restart the docker container: `docker stop nzbhydra && docker start nzbhydra`                      |
| Plex Requests - Meteor | Update within the app.                                                                         |
| Organizr               | Update within the app.                                                                         |
| Portainer              | TBA                                                                                            |
| UnionFS Cleaner        | Edit `/opt/unionfs_cleaner/config.json`. <br />  Set `"use_upload_manager"` to `true`.                              |