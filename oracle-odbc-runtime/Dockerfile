FROM bitnami/minideb:stretch
COPY oracle-instantclient12.2-basic-12.2.0.1.0-1.x86_64.rpm /
COPY oracle-instantclient12.2-odbc-12.2.0.1.0-2.x86_64.rpm /
RUN install_packages alien && \
    alien -i oracle-instantclient12.2-basic-12.2.0.1.0-1.x86_64.rpm && \
    alien -i oracle-instantclient12.2-odbc-12.2.0.1.0-2.x86_64.rpm && \
    apt-get remove --yes alien && \
    apt-get autoremove --yes && \
    install_packages libaio1 unixodbc libgmp10

ENV LD_LIBRARY_PATH=/usr/lib/oracle/12.2/client64/lib/
COPY odbcinst.ini /etc/odbcinst.ini

# Using isql requires a DSN configured via `odbc.ini`:
#
# [test]
# Driver = Oracle12
# DSN = test
# Password = <password>
# ServerName = //<host>:<port>/<db>
# UserID = <username>
#
# COPY odbc.ini /etc/odbc.ini
#
# To test, create the file by adding COPY from above, build the image
# and run:
#
#     docker run --rm -it oracle-odbc-runtime isql test
