docker-dcc-sourcebased
=======================
[![Build Status](https://travis-ci.org/ezh/docker-dcc-sourcebased.png?branch=master)](https://travis-ci.org/ezh/docker-dcc-sourcebased) [![Pulls](https://img.shields.io/docker/pulls/ezh1k/dcc.svg)](https://hub.docker.com/r/ezh1k/dcc/) [![Releases](https://img.shields.io/github/release/ezh/docker-dcc-sourcebased.svg)](https://github.com/ezh/docker-dcc-sourcebased/releases) [![License](https://img.shields.io/github/license/ezh/docker-dcc-sourcebased.svg)](https://github.com/ezh/docker-dcc-sourcebased/blob/master/LICENSE)

Source based DCC service based on Debian Jessie.

DCC build from source from https://www.dcc-servers.net/dcc/

By default it builds *dcc-1.3.159* if you use docker compose and *dcc-1.3.158* if you build directly from Dockerfile.

[Hint #1](https://github.com/ezh/docker-dcc-sourcebased/blob/master/docker/Dockerfile#L6),
[Hint #2](https://github.com/ezh/docker-dcc-sourcebased/blob/master/docker-compose.travis.yml#L7)

Image is based on `debian/jessie`, the same as an official Jenkis docker container.

Execution
---------

DCC is executed directly as PID 1 process with logging to `STDOUT`/`STDERR`.

Tips:

To find service command line:

1. edit `/dcc/conf/dcc_config` if needed

2. `docker run --rm -it dcc /bin/bash`

3. run suitable service
  * `/dcc/bin/start-dccd -a ...`
  * `/dcc/bin/start-dccifd -a ...`
  * `/dcc/bin/start-dccm -a ...`
  * `/dcc/bin/start-grey -a ...`

4. get default command line arguments with `ps -fp <PID> | cat`

5. adjust **command:** of `docker-compose.yml` like [this](https://github.com/ezh/docker-dcc-sourcebased/blob/master/docker-compose.yml)

DCC layout
----------

```
/dcc/bin
/dcc/cgi-bin
/dcc/conf
/dcc/log
```

Build parameters
----------------

You may alter build parameters of `DCC` with `dcc_config` argument.

Please look at Dockerfile for example.

Current DCC configuration:

```
--homedir=/dcc/conf
--bindir=/dcc/bin
--libexecdir=/dcc/bin
```

Copyright
---------

Copyright © 2017 Alexey B. Aksenov/Ezh. All rights reserved.
