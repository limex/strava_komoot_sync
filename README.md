# StravaKomootSync

Activity Synchronization between Strava and Komoot.
Synchronization direction: Strava --> Komoot

What is synced:
- Name of the activity
- Visibility (private, public)

## Script Parameter

    $GOPATH/bin/strava_komoot_sync -h

    Usage of ./strava_komoot_sync:
        -debug
                Log debug level
        -komoot_email string
                Komoot Email
        -komoot_pw string
                Komoot Password
        -komoot_userid string
                Komoot User ID
        -strava_athleteid int
                Strava Athlete ID
        -strava_clientid int
                Strava Client ID
        -strava_clientsecret string
                Strava Client Secret
        -strava_virtualRide_gearid string
                Strava Virtual Ride GearID
        -sync_all
                Sync all activities

Flag "-sync_all"
- true:  all activities will be synched once and program terminates
- false: the last 30 Strava activities will be synched

## Run Docker Container
### ... via Dockerfile

* Build and Run: 

        docker build --tag stravakomootsync:latest .
        docker run -d -p 8080:8080 --name stravakomootsync --restart unless-stopped -e 'KOMOOT_EMAIL=*****' -e 'KOMOOT_PWD=*****' -e 'KOMOOT_USERID=*****' -e 'STRAVA_CLIENTID=*****' -e 'STRAVA_CLIENTSECRET=*****' -e 'STRAVA_ATHLETEID=*****' -e 'STRAVA_VIRT_GEARID=*****' stravakomootsync

* Go to the Containers Tab in the Docker Desktop and select 'View Detail' at the "vertical hamburger".
* In the Logs Tab there will be are Link to Strava asking you to confirm the App Login. 
* This will sync the Names of the latest 30 Strava Activities with corresponding Komoot Activities.
Check Komoot to find your Activity Names updated.
* To update all Activities, add the parameter ...

        -e 'SYNC_ALL=true' 

  ... to aboves docker run command.

### ... via docker-compose and pre-build package from ghcr.io

[![Docker Image CI](https://github.com/aexel90/strava_komoot_sync/actions/workflows/docker-image.yml/badge.svg)](https://github.com/aexel90/strava_komoot_sync/actions/workflows/docker-image.yml)

WARNING!! This option is not working in this fork. It uses a precompiled package from the original repo with an error.

        cp .env.template .env
        vi .env
        docker compose up -d

## TODOs
- sync pics
