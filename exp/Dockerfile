FROM enonic/xp:7.3.1-ubuntu

# Set Memory settings
# Defaults to 1/4 of servers physical mem
# On single cpu
# ENV JAVA_OPTS "-Xms2G -Xmx2G"
# On multi cpu systems
# ENV JAVA_OPTS "-Xms3G -Xmx3G -Djsse.enableSNIExtension=true -XX:+UseConcMarkSweepGC -XX:+CMSParallelRemarkEnabled -XX:+UseCMSInitiatingOccupancyOnly -XX:CMSInitiatingOccupancyFraction=60 -XX:+ScavengeBeforeFullGC -XX:+CMSScavengeBeforeRemark"
# Dump memory to heapdum file on outofmem
ENV JAVA_OPTS="$JAVA_OPTS -XX:-HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/heapdump.hprof"

USER root
###############################################################################
#    Insert commands to place Enonic XP application in deploy folder here.    #
###############################################################################

# Either place the compiled jar file in the deploy folder...
COPY deploy/* $XP_ROOT/home/deploy/

###############################################################################
# configure
###############################################################################

RUN mkdir -p /enonic-xp/home/snapshots && chown $XP_USER /enonic-xp/home/snapshots
RUN mkdir -p /enonic-xp/home/work && chown $XP_USER /enonic-xp/home/work
RUN mkdir -p /enonic-xp/home/repo/ && chown $XP_USER /enonic-xp/home/repo
RUN mkdir -p /enonic-xp/home/data/ && chown $XP_USER /enonic-xp/home/data

COPY config/* $XP_ROOT/home/config/

COPY backup.sh /usr/local/bin/backup.sh
RUN chmod +x /usr/local/bin/backup.sh

RUN chown enonic-xp -R $XP_ROOT/home

EXPOSE 9200

USER enonic-xp
