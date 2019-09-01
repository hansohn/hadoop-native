# hadoop-native

This repository contains Hadoop **2.7.3** compiled native libraries for OSX.

### Components

The native hadoop library includes various components:

- Compression Codecs (bzip2, lz4, snappy, zlib)
- Native IO utilities for [HDFS Short-Circuit Local Reads](https://hadoop.apache.org/docs/r2.7.3/hadoop-project-dist/hadoop-hdfs/ShortCircuitLocalReads.html) and [Centralized Cache Management in HDFS](https://hadoop.apache.org/docs/r2.7.3/hadoop-project-dist/hadoop-hdfs/CentralizedCacheManagement.html)
- CRC32 checksum implementation

### Installation

Install compression codecs and copy over native hadoop libraries

```bash
# install compression codecs
$ brew install bzip2 gzip openssl snappy zlib

# copy libraries to hadoop home
$ cp -R ./hadoop-2.7.3/lib/native ${HADOOP_HOME}/lib/
```

Add environment variables to include hadoop native libraries

```bash
# add environment variables
export CLASSPATH=`${HADOOP_HOME}/bin/hadoop classpath --glob`
export DYLD_LIBRARY_PATH="${HADOOP_HOME}/lib/native/:${DYLD_LIBRARY_PATH}"
export HADOOP_COMMON_LIB_NATIVE_DIR=${HADOOP_HOME}/lib/native
export HADOOP_OPTS="-Djava.library.path=$HADOOP_HOME/lib/native ${HADOOP_OPTS}"
```

### Check

NativeLibraryChecker is a tool to check whether native libraries are loaded correctly. You can launch NativeLibraryChecker as follows:

``` bash
$ hadoop checknative -a
19/09/01 13:30:56 WARN bzip2.Bzip2Factory: Failed to load/initialize native-bzip2 library system-native, will use pure-Java version
19/09/01 13:30:56 INFO zlib.ZlibFactory: Successfully loaded & initialized native-zlib library
Native library checking:
hadoop:  true /usr/local/Cellar/hadoop/2.7.3/lib/native/libhadoop.dylib
zlib:    true /usr/lib/libz.1.dylib
snappy:  true /usr/local/lib/libsnappy.1.dylib
lz4:     true revision:99
bzip2:   false
openssl: true /usr/lib/libcrypto.35.dylib
19/09/01 13:30:56 INFO util.ExitUtil: Exiting with status 1
```

Please note that the bzip2 libraries do not compile into hadoop native properly on OSX. ([HADOOP-10409](https://issues.apache.org/jira/browse/HADOOP-10409))

### Documentation

The following resources may be helpful to better understand the native Hadoop library:

[NativeLibraries](https://hadoop.apache.org/docs/r2.7.3/hadoop-project-dist/hadoop-common/NativeLibraries.html)
