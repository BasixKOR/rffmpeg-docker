FROM panubo/sshd

# Install ffmpeg and hardware acceleration libraries
# nfs-utils is used for mounting the shared folder, which is a requirement for rffmpeg with jellyfin
RUN apk add --no-cache ffmpeg libva libva-intel-driver nfs-utils