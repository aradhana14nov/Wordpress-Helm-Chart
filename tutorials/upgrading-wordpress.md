## Upgrading WordPress

Because of its popularity, WordPress is often a target for malicious exploitation, so it’s important to keep it updated. We can upgrade Helm releases with the command helm upgrade.

To list all of your current releases, run the following command from your local machine or development server:

helm list
 
You should get output similar to this:

Output
NAME        REVISION    UPDATED                     STATUS      CHART           APP VERSION NAMESPACE
myblog      1           Fri Jan 25 20:24:10 2019    DEPLOYED    wordpress-5.1.2   5.0.3     default  

As you can see from the output, our current WordPress version is 5.0.3 (app version), while the chart version is 5.1.2. If you want to upgrade a release to a newer version of a chart, first update your Helm repositories with:

helm repo update
 
You can expect the following output:

Output
Hang tight while we grab the latest from your chart repositories...
...Skip local chart repository
...Successfully got an update from the "stable" chart repository
Update Complete. ⎈ Happy Helming!⎈ 
Now you can check if there’s a newer version of the WordPress chart available with:

helm inspect chart stable/wordpress
 
You should see output similar to this:

Output
apiVersion: v1
appVersion: 5.1.1
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
version: 5.9.0
As you can see from the output, there’s a new chart available (version 5.9.0) with WordPress 5.1.1 (app version). Whenever you want to upgrade your WordPress release to the latest WordPress chart, you should run:

helm upgrade -f values.yaml myblog stable/wordpress
 
This command will produce output very similar to the output produced by helm install. It is important to provide the same configuration file we used when installing the WordPress chart for the first time, as it contains the custom database settings we defined for our setup.

Now, if you run helm list again, you should see updated information about your release:

Output

NAME    REVISION    UPDATED                     STATUS      CHART           APP VERSION     NAMESPACE
myblog  2           Fri May  3 14:51:20 2019    DEPLOYED    wordpress-5.9.0   5.1.1         default  

You have successfully upgraded your WordPress to the latest version of the WordPress chart.

Rolling Back a Release
Each time you upgrade a release, a new revision of that release is created by Helm. A revision sets a fixed checkpoint to where you can come back if things don’t work as expected. It is similar to a commit in Git, because it creates a history of changes that can be compared and reverted. If something goes wrong during the upgrade process, you can always rollback to a previous revision of a given Helm release with the helm rollback command:

helm rollback release-name revision-number
 
For instance, if we want to undo the upgrade and rollback our WordPress release to its first version, we would use:

helm rollback myblog 1
 
This would rollback the WordPress installation to its first release. You should see the following output, indicating that the rollback was successful:

Output

Rollback was a success! Happy Helming!
Running helm list again should now indicate that WordPress was downgraded back to 5.0.3, chart version 5.1.2:

Output

NAME        REVISION    UPDATED                     STATUS      CHART           APP VERSION NAMESPACE
myblog      3       Mon Jan 28 22:02:42 2019    DEPLOYED    wordpress-5.1.2   5.0.3         default  

Notice that rolling back a release will actually create a new revision, based on the target revision of the roll-back. Our WordPress release named myblog now is at revision number three, which was based on revision number one.