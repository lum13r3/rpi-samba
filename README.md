Docker container that creates a SMB share.

## Running

```
docker run -d \
-p 137:137/udp \
-p 138:138/udp \
-p 139:139 \
-p 445:445 \
-p 445:445/udp \
--restart='always' \
--net=host \
-v /opt:/share/opt \
-v /:/share/ \
--name samba lum13r3/rpi-samba \
-u "niclas:-Maurice31-" \
-s "OPT Directory:/share/opt:rw:niclas" \
-s "MAIN Directory:/share/:rw:niclas"
```

## Build
```
docker build --rm --no-cache -t lum13r3/rpi-samba .
```

This example will bind `smbd` to docker host ip address
and mount two directories on docker host to container.
Additionally, the supplied hostname will be used for the NetBIOS name.
Two users will be created and given various access to four shares.
Ommitting users from a share results in guest access.
The `public` share will have guest access and be browsable.

## Connecting
You'll want to expose enough ports to make the server discoverable.
The example above should be enough to get you moving.

Open Finder, then press âŒ˜K. Enter `smb://<docker_host_ip>`
and press `Connect`.
Enter login and password you supplied at the run stage.
