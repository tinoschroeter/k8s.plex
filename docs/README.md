# Plex Media Server

[![Build Status](https://jenkins.tino.sh/buildStatus/icon?job=k8s.plex%2Fmaster)](https://jenkins.tino.sh/job/k8s.plex/job/master/)
[![k3s](https://img.shields.io/badge/run%20on%20-Raspberry%20Pi-red)](https://github.com/tinoschroeter/k8s.homelab)
[![GitHub Super-Linter](https://github.com/tinoschroeter/k8s.plex/workflows/Lint%20Code%20Base/badge.svg)](https://github.com/tinoschroeter/k8s.plex/actions/workflows/linter.yml)

[Plex](https://plex.tv) organizes video, music and photos from personal media libraries and streams them to smart TVs, streaming boxes and mobile devices. This container is packaged as a standalone Plex Media Server. has always been a top priority. Straightforward design and bulk actions mean getting things done faster.


[![plex](http://the-gadgeteer.com/wp-content/uploads/2015/10/plex-logo-e1446990678679.png)](https://plex.tv)

- **HOSTNAME** Sets the hostname inside the docker container. For example `-h PlexServer` will set the servername to `PlexServer`. Not needed in Host Networking.
- **TZ** Set the timezone inside the container.  For example: `Europe/London`.  The complete list can be found here: [https://en.wikipedia.org/wiki/List_of_tz_database_time_zones](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)
- **PLEX_CLAIM** The claim token for the server to obtain a real server token.  
  If not provided, server will not be automatically logged in.  If server is already logged in, this parameter is ignored.  
  You can obtain a claim token to login your server to your plex account by visiting [https://www.plex.tv/claim](https://www.plex.tv/claim)
- **ADVERTISE_IP** This variable defines the additional IPs on which the server may be found.  For example: `http://10.1.1.23:32400`.  
  This adds to the list where the server advertises that it can be found.  This is only needed in Bridge Networking.

These parameters are usually not required but some special setups may benefit from their use.  
As in the previous section, each is treated as first-run parameters only:

- **PLEX_UID** The user ID of the `plex` user created inside the container.
- **PLEX_GID** The group ID of the `plex` group created inside the container
- **CHANGE_CONFIG_DIR_OWNERSHIP** Change ownership of config directory to the plex user.  Defaults to `true`.  
  If you are certain permissions are already set such that the `plex` user within the container can read/write data in it's config directory, 
  you can set this to `false` to speed up the first run of the container.
- **ALLOWED_NETWORKS** IP/netmask entries which allow access to the server without requiring authorization. We recommend you set this only if you do not sign in your server.
  For example `192.168.1.0/24,172.16.0.0/16` will allow access to the entire `192.168.1.x` range and the `172.16.x.x` range.  
  Note: If you are using Bridge networking, then localhost will appear to plex as coming from the docker networking gateway which is often `172.16.0.1`.
