By default, watchtower will watch all containers. However, sometimes only some containers should be updated.

If you need to exclude some containers, set the _com.centurylinklabs.watchtower.enable_ label to `false`.

```docker
LABEL com.centurylinklabs.watchtower.enable="false"
```

Or, it can be specified as part of the `docker run` command line:

```bash
docker run -d --label=com.centurylinklabs.watchtower.enable=false someimage
```

If you need to [include only containers with the enable label](https://containrrr.github.io/watchtower/arguments/#filter_by_enable_label), pass the `--label-enable` flag or the `WATCHTOWER_LABEL_ENABLE` environment variable on startup and set the _com.centurylinklabs.watchtower.enable_ label with a value of `true` for the containers you want to watch.

```docker
LABEL com.centurylinklabs.watchtower.enable="true"
```

Or, it can be specified as part of the `docker run` command line:

```bash
docker run -d --label=com.centurylinklabs.watchtower.enable=true someimage
```

If watchtower is monitoring the same Docker daemon under which the watchtower container itself is running (i.e. if you volume-mounted _/var/run/docker.sock_ into the watchtower container) then it has the ability to update itself. If a new version of the _containrrr/watchtower_ image is pushed to the Docker Hub, your watchtower will pull down the new image and restart itself automatically.
