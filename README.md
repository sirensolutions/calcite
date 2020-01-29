<!--
{% comment %}
Licensed to the Apache Software Foundation (ASF) under one or more
contributor license agreements.  See the NOTICE file distributed with
this work for additional information regarding copyright ownership.
The ASF licenses this file to you under the Apache License, Version 2.0
(the "License"); you may not use this file except in compliance with
the License.  You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
{% endcomment %}
-->
[![Travis Build Status](https://travis-ci.org/apache/calcite.svg?branch=master)](https://travis-ci.org/apache/calcite)
[![AppVeyor Build Status](https://ci.appveyor.com/api/projects/status/github/apache/calcite?svg=true&branch=master)](https://ci.appveyor.com/project/ApacheSoftwareFoundation/calcite)

# Apache Calcite

Apache Calcite is a dynamic data management framework.

For more details, see the [home page](http://calcite.apache.org).

# Siren Deployment 
## For Development
When developing and testing new features, one can use Maven SNAPSHOT feature to deploy over and over on artifactory.
To set this up, change the version in all pom.xml to append `-SNAPSHOT`.

For instance in the pom.xml it should look like this:
```xml
...
  <!-- The basics. -->
  <groupId>org.apache.calcite</groupId>
  <artifactId>calcite</artifactId>
  <packaging>pom</packaging>
  <version>1.19.0-siren-0.1.0-SNAPSHOT</version>
...
```

Once all the POM files are set, one can run these 2 commands to install and then to deploy to Siren Artifactory repository `libs-snapshot-local`.
```bash
mvn -P artifactory -DskipTests \
  -Dartifactory_username=$ARTIFACTORY_USERNAME \
  -Dartifactory_password=$ARTIFACTORY_API_KEY \
  clean install

mvn -P artifactory -DskipTests \
  -Dartifactory_username=$ARTIFACTORY_USERNAME \
  -Dartifactory_password=$ARTIFACTORY_API_KEY \
  deploy
```

`-Dcheckstyle.skip` allows one to install without checking style failing.

## For Production Release
Change all the version in POM files to the release version and use the same command. 
Maven will figure out from the name convention that it deploys the release to a different Artifactory repository
as defined in the main pom.xml file section called `distributionManagement`.
