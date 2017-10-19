# odbc-stack-build

This image is based on [fpco/stack-build][stack-build] and includes
`unixODBC` libraries required to build Haskell Stack projects using
[HDBC-odbc][].

To use it, put the following in your `stack.yaml`:

    resolver: lts-9.9
    docker:
      repo: atom/odbc-stack-build

Now you can build your project with `stack --docker build`.

[hdbc-odbc]: http://hackage.haskell.org/package/HDBC-odbc
[stack-build]: https://hub.docker.com/r/fpco/stack-build/
