# Uninstall a Release
To uninstall a release, use the helm uninstall command:

$ helm uninstall smiling-penguin
Removed smiling-penguin
This will uninstall smiling-penguin from Kubernetes, which will remove all resources associated with the release as well as the release history.

If the flag --keep-history is provided, release history will be kept. You will be able to request information about that release:

$ helm status smiling-penguin
Status: UNINSTALLED