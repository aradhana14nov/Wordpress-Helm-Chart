# Uninstall the Chart

To uninstall the wordpress helm chart, use the helm delete command:

$ helm delete wordpress -n wordpress

The command removes all the Kubernetes components associated with the chart and deletes the release.


$ helm status wordpress -n wordpress
Status: UNINSTALLED