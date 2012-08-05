## Deploying to Sonatype's snapshot repository

```sh
ant -lib build/lib snapshot.maven
```

## Building JARs and ZIPs for upload to GitHub

```sh
ant -lib build/lib -Dversion-status=-SNAPSHOT-20120805-1225 zip
```

Replace `20120805-1225` with the current date and time.