## SQL*Plus Docker image

Forked from  forked from [guywithnose/docker-sqlplus](https://github.com/guywithnose/docker-sqlplus)
and inspired by [thriqon/docker-sqlplus](https://github.com/thriqon/docker-sqlplus).

This is a modified SQL*Plus docker image i've done in order to be enable to
use my own [tnsnames.ora](https://docs.oracle.com/cd/B28359_01/network.111/b28317/tnsnames.htm)
and a dir where I could put some scripts.

Build it like this:
`docker build . -t plus`

Connect to a running Oracle database like this

`docker run --interactive -e USERNAME=username -e PASSWORD=password -e NET_SERVICE_NAME=XE -v /host/scripts/dir:/usr/workdir -v /host/oracle_home/network/admin:/usr/network/admin --net="host" plus`

If the target database is inside another container you can link it:
`docker run --interactive --link database_container_name:name_of_database_host_in_tnsnames_dot_ora -e USERNAME=username -e PASSWORD=password -e NET_SERVICE_NAME=XE -v /host/scripts/dir:/usr/workdir -v /host/oracle_home/network/admin:/usr/network/admin plus`

Where:
* _username_ is your user name.
* _XE_ is the net service name for the target database in your `tnsnames.ora`.
* _/host/scripts/dir_ is your local dir where you have the scripts that you need to be visibles by sqlplus.
* _/host/oracle_home/network/admin_ is your local $ORACLE_HOME/network/admin or the dir where you have your `tnsnames.ora`.

In order to avoid the presence of password in your history commands i've intentionally omitted the password param so you will be prompted for it by sqlplus.
