## Releasing Snapshots

### Deploying to Sonatype's snapshot repository

```sh
ant -lib build/lib snapshot.maven
```

### Building JARs and ZIP for upload to GitHub

```sh
ant -lib build/lib -Dversion-status=-SNAPSHOT-20120805-1225 zip
```

Replace `20120805-1225` with the current date and time.


## Releasing a beta version

### Deploying to Sonatype's staging repository

```sh
ant -lib build/lib -Dversion-status=-beta-1 stage.maven
```
Replace `-beta-1` as appropriate.

Release it: https://docs.sonatype.org/display/Repository/Sonatype+OSS+Maven+Repository+Usage+Guide#SonatypeOSSMavenRepositoryUsageGuide-8a.ReleaseIt

### Building JARs and ZIP for upload to GitHub

```sh
ant -lib build/lib -Dversion-status=-beta-1 zip
```