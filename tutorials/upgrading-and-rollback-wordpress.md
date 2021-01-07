---
title: How to Upgrade and Rollback WordPress chart 
description: This tutorial explains how to Upgrade and Rollback WordPress helm chart
---



### Upgrading WordPress

It is also important to keep WordPress helm chart updated. 

To Upgrade wordpress helm chart,Please execute following steps:

Step 1: To list all of your current releases, run the following command :

```execute
helm list
``` 
You should get output similar to this:

Output
NAME        REVISION    UPDATED                     STATUS      CHART           APP VERSION NAMESPACE
wordpress      1           Tue Jan 5 20:24:10 2021    DEPLOYED    wordpress-10.0.1   5.5.3     wordpress

As you can see from the output, our current WordPress version is 5.5.3 (app version), while the chart version is 10.0.1. 

Step 2: Update your Helm repositories with following command :

```execute
helm repo update
```
 
You can expect the following output:

Output
Hang tight while we grab the latest from your chart repositories...
...Skip local chart repository
...Successfully got an update from the "stable" chart repository
Update Complete. ⎈ Happy Helming!⎈ 


Step 3: Check if there’s a newer version of the WordPress chart available using following command:

```execute
helm inspect chart bitnami/wordpress
``` 

You should see output similar to this:

```
apiVersion: v1
appVersion: 5.5.3
description: Web publishing platform for building blogs and websites.
engine: gotpl
home: http://www.wordpress.com/
icon: https://bitnami.com/assets/stacks/wordpress/img/wordpress-stack-220x234.png
keywords:
- wordpress
- cms
- blog
- http
- web
- application
- php
maintainers:
- email: containers@bitnami.com
  name: Bitnami
name: wordpress
sources:
- https://github.com/bitnami/bitnami-docker-wordpress
version: 10.0.3
```

As you can see from the output, there’s a new chart available (version 10.0.3) with WordPress 5.5.3 (app version). 

Step 4: To upgrade your WordPress release to the latest WordPress chart, execute below command:

```execute
helm upgrade wordpress -f wordpress-values.yaml bitnami/wordpress --namespace wordpress
```
 
This command will produce output very similar to the output produced by helm install. It is important to provide the same configuration file we used when installing the WordPress chart for the first time, as it contains the custom database settings we defined for our setup.

Step 5: Check updated information about your release using helm list command.

```execute
helm list
``` 

Output
```
NAME    REVISION    UPDATED                     STATUS      CHART           APP VERSION     NAMESPACE
wordpress  2           Tue Jan 5  21:51:20 2021    DEPLOYED    wordpress-5.5.3   10.0.3         wordpress
```

You have successfully upgraded your WordPress to the latest version of the WordPress chart.


### Rolling Back a Release

Each time you upgrade a release, a new revision of that release is created by Helm. A revision sets a fixed checkpoint to where you can come back if things don’t work as expected. 
If something goes wrong during the upgrade process, you can always rollback to a previous revision of a given Helm release with the helm rollback command.


If we want to undo the upgrade and rollback our WordPress release to its previous version, execute following command:

Step 1: execute rollback command :

```execute
helm rollback wordpress 1
```

Output:
```
Rollback was a success! Happy Helming!
```
 
This would rollback the WordPress installation to its previous release. 

Step 2: Check WordPress was downgraded back to 10.0.3, chart version 5.5.3:

```execute
helm list
``` 

Output:

```
NAME        REVISION    UPDATED                     STATUS      CHART           APP VERSION NAMESPACE
wordpress      3      Tue Jan 5 22:02:42 2021    DEPLOYED    wordpress-10.1.2   10.0.3         default  
```

Notice that rolling back a release will actually create a new revision, based on the target revision of the roll-back. Our WordPress release named wordpress now is at revision number 3, which was based on revision number 1.
