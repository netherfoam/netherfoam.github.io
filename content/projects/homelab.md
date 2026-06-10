+++
title = '⚙️️ Homelab'
date = 2026-06-10
draft = false
description = 'Self-hosted media server and compute node. Docker, mdadm RAID, nginx reverse proxy, mDNS, Home Assistant, Plex, Immich.'
+++


# Homelab

---

## Motivation

A few things converged: multiplayer game servers cost real money to rent and the hardware you get is usually disappointing;
streaming services kept raising prices while I had no ownership of anything I paid for; and I needed somewhere to store
and process the terabytes of spatial data that come with GIS development work. Building a server solved all three at once.

## Hardware

| Component   | Spec                                              |
|-------------|---------------------------------------------------|
| CPU         | AMD Ryzen 7 5800X3D                               |
| RAM         | 64 GB                                             |
| Root drive  | NVMe M.2 SSD                                      |
| Storage     | 3 × 8 TB CMR HDDs in mdadm RAID 5 (~16 TB usable) |
| GPU         | Low-profile discrete GPU                          |
| Form factor | mATX mini tower                                   |

The server is headless - no monitor, no keyboard. SSH is the only way in. It runs continuously.

The 5800X3D's 3D V-Cache makes it exceptional for cache-sensitive workloads. Factorio runs noticeably better than the 
clock speed alone would suggest. The GPU is too weak to assist Plex transcoding in any meaningful way, was simply 
included because the X3D chip doesn't have integrated graphics.

## Infrastructure

**Containerisation:** All services run in Docker, defined as Compose stacks and managed through Portainer. Stack
definitions are version-controlled in a private GitHub repository. Secrets live in host-side env files excluded from
Git and injected at deploy time.

**Reverse proxy:** Rather than manually maintaining proxy config, I use an nginx container that reads hostname and port
environment variables off sibling containers and generates configuration automatically. Adding a new service to the LAN
requires two environment variables and a restart - no manual nginx config involved - and an mDNS advertisement on the
host.

**Local DNS:** I deliberately chose not to run a DNS server. A dedicated resolver is a network-wide single point of
failure - if it goes down, nothing resolves. Instead, I use mDNS via Avahi to advertise `.local` hostnames on the LAN.
Services like `plex.local` just work in any browser on the network with no client configuration required.

## Service Stack

| Category              | Services                                                 |
|-----------------------|----------------------------------------------------------|
| Media serving         | Plex                                                     |
| Home automation       | Home Assistant, Mosquitto (MQTT)                         |
| Photos                | Immich                                                   |
| Monitoring            | Beszel                                                   |
| GIS compute           | Dask                                                     |
| Game servers (ad hoc) | Factorio, Valheim, Ark Survival Ascended, Stardew Valley |

## Backup

Media files and other re-downloadable content are excluded from backups - there's no value in backing up what can be
re-acquired. What gets backed up is configuration, databases, and irreplaceable personal data. Live databases require
pre-dump snapshots rather than filesystem snapshots to avoid backing up mid-write state. I use Restic to create backup
snapshots. 

### Destroying an entire RAID Array

After a power supply failed, I replaced it and learned mixing cables from modular power supplies, although the pins
physically fit, will destroy equipment. I discovered this after frying an entire RAID array of disk drives during the
drive shortage in 2026. That hurt to learn - and my backups were a year old! Fortunately I recovered data from most
sources. I knew I needed to do backups more often, but I was lazy and the effort was high.

RAID protects against a drive failure. It doesn't protect against human error, accidental deletion, or, apparently,
mixing modular PSU cables. Who'd have thought?

Well, that pushed me to create a bash script run on every SSH connection to check if a backup was needed. If it has been a while since my last
backup, I'm now prompted with a simple `31 days since last backup` and `Backup now? [y/n]`. That mounts my external
drive (or complains the drive is unplugged) and begins the backup sequence. This way, I don't need to remember to do
anything except occasionally SSH in (I do that anyway) and plug in the backup drive. 

I've said for a long time for my career: Make it so doing the right thing is the easy thing to do. I'm no exception to
the rule.

