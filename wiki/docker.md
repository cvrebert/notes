* Name your images: `docker build --tag name-goes-here .`
* Name your containers: `docker run --name rorschach some-image`
* For non-daemons, you probably want:
  * `docker run --rm=true some-image` to avoid temporary containers from piling up and hogging all your disk space
  * `ENTRYPOINT ["/path/to/the/binary"]` (instead of `CMD`)
* Don't get `CMD` and `RUN` mixed up.
  * At most one `CMD` per Dockerfile
  * `RUN` is for setup steps
* `chmod` must happen **AFTER** `chown`, due to https://github.com/docker/docker/issues/6047
