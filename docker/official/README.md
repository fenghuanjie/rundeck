
## start with persistent storage

The simplest way to persist data between container starts/upgrades is to
utilize named volumes:  
`$ docker run --name some-rundeck -v data:/home/rundeck/server/data`

## control JVM heap allocation

`$ docker run -m 1024m`

The JVM is configured to use cgroup information to set the max heap allocation size.
The RAM ration is set to `1`, so the JVM will utilize up to about the container limit.

## Environment Variables

### `RUNDECK_GRAILS_URL=http://127.0.0.1:4440`

Controls the base URL the app will use for links, redirects, etc.
This is the URL users will use to access the site.

### `RUNDECK_SERVER_ADDRESS=0.0.0.0`

This is the address or hostname the application will attempt to bind to within
the container.

### `RUNDECK_DATABASE_URL`

Defaults to `jdbc:h2:file:/home/rundeck/server/data/grailsdb;MVCC=true`. The default configuration utilizes an h2 file for data storage.

### `RUNDECK_DATABASE_DRIVER`

Set this if using an alternative backend from h2.

- `org.postgresql.Driver`
- `org.mariadb.jdbc.Driver`
- `com.mysql.jdbc.Driver`

### `RUNDECK_DATABASE_USERNAME`

### `RUNDECK_DATABASE_PASSWORD`

### `RUNDECK_LOGGING_STRATEGY=CONSOLE`

The default console strategy configures log4j to send all output to stdout
to be collected by the container logging driver.

Set to `FILE` to log into `/home/rundeck/server/logs` .

### `RUNDECK_LOGGING_AUDIT_ENABLED`

Set to anything enables audit logging. This can be very verbose so use with caution.