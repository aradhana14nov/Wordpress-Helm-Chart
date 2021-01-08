---
title: How to Upgrade and Rollback WordPress chart 
description: This tutorial explains how to Upgrade and Rollback WordPress helm chart
---



### Upgrading WordPress

It is also important to keep WordPress helm chart updated. 

To Upgrade wordpress helm chart,Please execute following steps:

Step 1: To list all of your current releases in namespace "wordpress", run the following command :

```execute
helm list -n wordpress
``` 
You should get output similar to this:

Output:
```
NAME            NAMESPACE       REVISION        UPDATED                                 STATUS       CHART            APP VERSION
wordpress       wordpress       1               2021-01-07 03:02:43.441726889 -0600 CST deployed     wordpress-10.3.1 5.6.0      
```
 
As you can see from the output, our current WordPress version is 5.6.0 (app version), while the chart version is 10.3.1 which is the latest one.
But suppose our current helm chart version is 10.1.0 and app version is 5.6.0 and is not updated one and we need to upgrade it.We need to follow below steps.

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
helm search repo wordpress --versions
``` 

You should see output similar to this:

```
NAME                    CHART VERSION   APP VERSION     DESCRIPTION                                       
bitnami/wordpress       10.3.1          5.6.0           Web publishing platform for building blogs and ...
bitnami/wordpress       10.3.0          5.6.0           Web publishing platform for building blogs and ...
bitnami/wordpress       10.2.1          5.6.0           Web publishing platform for building blogs and ...
bitnami/wordpress       10.2.0          5.6.0           Web publishing platform for building blogs and ...
bitnami/wordpress       10.1.5          5.6.0           Web publishing platform for building blogs and ...
bitnami/wordpress       10.1.4          5.6.0           Web publishing platform for building blogs and ...
bitnami/wordpress       10.1.2          5.6.0           Web publishing platform for building blogs and ...
bitnami/wordpress       10.1.1          5.6.0           Web publishing platform for building blogs and ...
bitnami/wordpress       10.1.0          5.6.0           Web publishing platform for building blogs and ...
bitnami/wordpress       10.0.10         5.6.0           Web publishing platform for building blogs and ...
bitnami/wordpress       10.0.9          5.6.0           Web publishing platform for building blogs and ...
bitnami/wordpress       10.0.8          5.5.3           Web publishing platform for building blogs and ...
bitnami/wordpress       10.0.7          5.5.3           Web publishing platform for building blogs and ...
bitnami/wordpress       10.0.6          5.5.3           Web publishing platform for building blogs and ...
bitnami/wordpress       10.0.5          5.5.3           Web publishing platform for building blogs and ...
bitnami/wordpress       10.0.3          5.5.3           Web publishing platform for building blogs and ...
```

As you can see from the output, there’s a new chart available (version 10.3.1) with WordPress 5.6.0 (app version). 

Step 4: To upgrade your WordPress release to the latest WordPress chart, execute below command:

```execute
cd /home/student/projects/Wordpress-Helm-Chart/
helm upgrade wordpress -f wordpress-values.yaml bitnami/wordpress --namespace wordpress
```
 
This command will produce output very similar to the output produced by helm install. It is important to provide the same configuration file we used when installing the WordPress chart for the first time, as it contains the custom database settings we defined for our setup.

Step 5: Check updated information about your release using helm list command.

```execute
helm list -n wordpress
``` 

Output
```
NAME            NAMESPACE       REVISION        UPDATED                                 STATUS       CHART            APP VERSION
wordpress       wordpress       2               2021-01-07 04:02:43.441726889 -0600 CST deployed     wordpress-10.3.1 5.6.0    
```

You have successfully upgraded your WordPress to the latest version of the WordPress chart.


### Rolling Back a Release

Each time you upgrade a release, a new revision of that release is created by Helm. A revision sets a fixed checkpoint to where you can come back if things don’t work as expected. 
If something goes wrong during the upgrade process, you can always rollback to a previous revision of a given Helm release with the helm rollback command.


If we want to undo the upgrade and rollback our WordPress release to its previous version, execute following command:

Step 1: execute rollback command :

```execute
helm rollback wordpress 1 -n wordpress
```

Output:
```
Rollback was a success! Happy Helming!
```
 
This would rollback the WordPress installation to its previous release. 

Step 2: Check WordPress was downgraded back to previous version:

```execute
helm list -n wordpress
``` 

Output:

```
NAME            NAMESPACE       REVISION        UPDATED                                 STATUS       CHART            APP VERSION
wordpress       wordpress       3               2021-01-07 04:02:43.441726889 -0600 CST deployed     wordpress-10.1.0 5.6.0    
```

Notice that rolling back a release will actually create a new revision, based on the target revision of the roll-back. Our WordPress release named wordpress now is at revision number 3, which was based on revision number 1.
