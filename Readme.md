# Compose Files
 multiple compose files used with Docker & Podman for multiple images. Images included are:
- Archivebox
- Forgejo
- Miniflux
- Nginx
- PostgreSQL
- MongoDB
- Redis
- ValKey


## How-To

### Extract podman images to save bandwidth
You can save podman images to save bandwidth, and prevent podman from automatically deleting them if they were not used for a lot of time. This especially good if you're using a very big image (like archivebox, which is around 700MB), beside using an exact version that you don't want to upgrade in a very frequent way.

- list images: `$ podman images`
- Export a pulled image to a `.tar` file using: `$ podman save -o myimage.tar <image-name>`.
	- you can get the image name from your compose file in the image field, and of course you need to type the version, like: `docker.io/library/postgres:17.5-bullseye`
	- I prefere to have a convention for naming exported images and I recommend to: `${image-source}-${image-name}-${image-version}.tar` --> like `codeberg.org-forgejo-14.0.2.tar` & `docker.io-postgres-17.5-bullseye.tar`. You can get image name
- Then you can load it to Podman to be able to use it: `$ podman load -i ~/path-to-images/my-image.tar`, and verify its availability: `$ podman images`
- then run your compose file again and it'll not redownload the image.