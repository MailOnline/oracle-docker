# oracle-odbc-runtime

A small image to get Oracle connection working using unixODBC.
Suitable for apps using [HDBC-odbc][hdbc-odbc].

## Building the image

1. Download [Oracle libraries][oracle-libs] in the same directory
as this Dockerfile. You need Basic and ODBC packages.

        oracle-instantclient12.2-basic-12.2.0.1.0-1.x86_64.rpm
        oracle-instantclient12.2-odbc-12.2.0.1.0-2.x86_64.rpm

2. Build the image

        docker build -t oracle-odbc-runtime .

The Oracle driver is registered with unixODBC manager under `Oracle12`
name.

ODBC connection string example using this image would be:

    Driver=Oracle12;PWD=<password>;UID=<username>;DBQ=//<host>:<port>/<db>

## Using the image with Haskell Stack

Put the following in your `stack.yaml`:

    image:
      containers:
        - base: oracle-odbc-runtime

Now building your project container with `stack image container` will
use your locally built `oracle-odbc-runtime` as a base image.

In your code, connect to Oracle like this:

```haskell
import Database.Persist
import Database.Persist.ODBC

...

main = do
  let connString = "Driver=Oracle12;..."
  withODBCConn (Just oracleMin12c) connString $ runSqlConn $
    ...
```

[hdbc-odbc]: http://hackage.haskell.org/package/HDBC-odbc
[oracle-libs]: http://www.oracle.com/technetwork/database/features/instant-client/index-097480.html
