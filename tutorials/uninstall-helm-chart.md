---
title: How to Uninstall WordPress chart 
description: This tutorial explains how to Uninstall WordPress helm chart
---

### Uninstall WordPress Helm Chart

To uninstall the wordpress helm chart, use the helm delete command:

```execute
helm delete wordpress -n wordpress
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

```execute
helm status wordpress -n wordpress
```

Output:

```
Status: UNINSTALLED
```
