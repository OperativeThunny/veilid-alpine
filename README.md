# veilid-alpine
alpine based container running veilid with auto update from an alpine package. 

## requirements from DilDog:

```
others have tried and the configuration was kind of insufficient. Goals: get Direct dialinfo when possible and not require a relay, and most docker containers end up running with some undesirable level of NAT. should have ports forwarded correctly. should work with ipv4 and ipv6 when available. should work with standard networking and --net=host.
should also ensure the latest version of veilid-server is installed and when new versions are available it should automatically upgrade them and restart veilid-server without having to kill the container
veilid-cli is tricky as well, as we have moved to IPC-based connections for that, so passing that through to docker may be tricky or not doable. it can be done with docker exec into the container though so make sure veilid-cli is in there too.
anyway, sorry for all the requirements but if it's just a simple dockerfile that runs the thing we aren't going to publish that because it would cause more problems than it solves for the network, which wants unattended upgrades of the veilid-server because literally 50% of our server operators don't upgrade when a new version is made available until they get around to it.
```

and

```
good luck. it should build on musl linux.
(at least it did at one point)
and thanks! getting things running on alpine would be useful 
happy to provide feedback, sure 🙂
the earlier requirements were just to give you an idea of the scope involved
if you want to help get an actual alpine build working, before worrying about dockerizing it with alpine, that would be better
we do the build for linux using Earthly
If you want to help, take a look at Earthly and look at our Earthfile in the veilid repo
that's our containerized build system. If you've not used Earthly before, you'll have to learn it to contribute there.
but if you want to make an 'package-linux-arm64-apk' and 'package-linux-amd64-apk' target for that Earthfile that produces the appropriate packages, we can stand up a place to distribute them, which would make a dockerized build for Alpine more tractable for people.
otherwise, make the docker container use Debian or something else that has an official build. i think building veilid inside the container itself is a non-starter.
```

# TODO:
  - [ ]  pingas
- [ ]  pongas
- [ ]  build veilid with musl based linux (alpine satisfies this)
- [ ]  package veilid server with veilid cli into an APK
- [ ]  get apk published
- [ ]  set up automation to `git pull --all` and rebuild the apk with the latest veilid and republish the apk
- [ ]  create Earthly/Earthfile to make a veilid container that runs supervisorD to keep the veilid-server running and provide an option for a web interface if the administrator of the server that is running the container wishes.
- [ ]  set up cronjob with supervisorD inside the container to automatically pull the latest APK and install it so then the veilid network can be healthier
- [ ]  publish everything
- [ ]  ???
- [ ]  get money
