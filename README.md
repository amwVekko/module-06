# module-06
Artifact Repository Manager with Nexus

Install and Run Nexus on a cloud server
1. created new droplet, because nexus needs more ressources: FRA1, ubuntu 22.10, 4 CPUS, 8GB RAM
2. assigned firewall with port 22, 8081
3. apt update && apt dist-upgrade -y && apt install openjdk-8-jre-headless -y
4. rebooted server as new kernel was installed
5. wget https://download.sonatype.com/nexus/3/nexus-3.61.0-02-unix.tar.gz
6. tar -zxvf nexus-3.61.0-02-unix.tar.gz
7. adduser nexus
8. chown -R nexus:nexus nexus-3.61.0-02 sonatype-work
9. edited nexus.rc to run application as nexus user
10. started app as nexus user: su - nexus. /opt/nexus-3.61.0-02/bin/nexus start
11. looked for admin pw at cat /opt/sonatype-work/nexus3/admin.password
12. ran config wizard of nexus
---------------------------------------------
Publish Artifact to Repo
1. added personal user in nexus app with new role
2. in project java-app added plugin 'maven-publish' with publications and repositories.
3. added gradle.properties file with user and password
4. gradle build and gradle publish
5. checked files in nexus
6. switched to java-maven-app
7. added settings.xml in user dir
8. added distributionManagement in pom.xml
9. build app with maven package
10. published to nexus with mvn deploy
11. checked files in nexus
---------------------------------------------
Nexus API
1. requesting api with curl -u user:pwd -X GET 'http://"dropletIPv4":8081/service/rest/v1/respositories' (User and password created in topic above)
2. admin will see all repos, because of access rights
3. files in maven snapshots will be shown with curl -u user:pwd -X GET 'http://"dropletIPv4":8081/service/rest/v1/componets?respository=maven-snapshots'
---------------------------------------------
Blob Store
1. created blobstore with type=file path=blobs/mystore

---------------------------------------------
Cleanup policies and scheduled tasks
1. created cleanup policie: name=maven format=maven2 asset_name_matcher=".*"
2. assinged cleanup policie to repo maven-snapshots
3. checked if tasks for cleanup got created
4. created admin blob compact task to run daily at 06:00 CET
5. started cleanup manually. no more files in repo found
6. started compact-store task to cleanup default blob store, files got deleted from disk




Reference: DevOps Bootcamp and TWN
