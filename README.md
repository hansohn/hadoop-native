# hadoop-native

This repository contains Hadoop **2.7.3** compiled native libraries for OSX.

### Installation

Copy lib native directory to hadoop home

```bash
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
