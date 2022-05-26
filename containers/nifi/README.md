<!--
  Licensed to the Apache Software Foundation (ASF) under one or more
  contributor license agreements.  See the NOTICE file distributed with
  this work for additional information regarding copyright ownership.
  The ASF licenses this file to You under the Apache License, Version 2.0
  (the "License"); you may not use this file except in compliance with
  the License.  You may obtain a copy of the License at
      http://www.apache.org/licenses/LICENSE-2.0
  Unless required by applicable law or agreed to in writing, software
  distributed under the License is distributed on an "AS IS" BASIS,
  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
  See the License for the specific language governing permissions and
  limitations under the License.
-->

# Docker Image for OpenShift

This image can be used directly on OpenShift without needing any specific SCC or capabilities. File ownership conforms to OpenShift standard, allowing the image to be used in any namespace, whatever the Service Account uid.

The image is based on [ubi8/openjdk-11](https://catalog.redhat.com/software/containers/ubi8/openjdk-11/5dd6a4b45a13461646f677f4)

## Latest changes

### 1.14.0

- Updated default container configuration to use HTTPS with Single User Authentication

### 1.12.0
- The NiFi Toolkit has been added to the image under the path `/opt/nifi/nifi-toolkit-current` also set as the environment variable `NIFI_TOOLKIT_HOME`
- The installation directory and related environment variables are changed to be version-agnostic to `/opt/nifi/nifi-current`:
```
docker run --rm --entrypoint /bin/bash apache/nifi:1.12.0 -c 'env | grep NIFI'
NIFI_HOME=/opt/nifi/nifi-current
NIFI_LOG_DIR=/opt/nifi/nifi-current/logs
NIFI_TOOLKIT_HOME=/opt/nifi/nifi-toolkit-current
NIFI_PID_DIR=/opt/nifi/nifi-current/run
NIFI_BASE_DIR=/opt/nifi
```
- A symlink refer to the new path for backward compatibility:
```
docker run --rm --entrypoint /bin/bash apache/nifi:1.12.0 -c 'readlink /opt/nifi/nifi-1.12.0'                                   /opt/nifi/nifi-current
```
