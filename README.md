# rffmpeg-server

This is a very simple Docker image for spinning up your own rffmpeg server.

## Setting up NFS volume
```sh
docker volume create --driver local \
  --opt type=nfs \
  --opt o=addr=[ip-address],rw \
  --opt device=:[path-to-directory] \
  video
```

You may need to change the option according to your environment.

## Spinning up the container

### Intel CPU Hardware Acceleration
```sh
docker run -d --name=rffmpeg -v \
    $(pwd)/rffmpeg_authorized_keys:/etc/authorized_keys/jellyfin:z \ # Path to authorized_keys.
	-v video:/volume1/video \ # Mount the video directory. You would want to set up a NFS volume here.
	-e "SSH_USERS=jellyfin:1000:1000" \ 
	-p 22:22
	--device /dev/dri/card0 \ # These device options are required for the hardware acceleration.
	--device /dev/dri/renderD128
	rtyu1120/rffmpeg-server:intel
```