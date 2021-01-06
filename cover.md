<h1 align="center">WordPress Operator</h1>

![Logo](_images/logo.PNG)

WordPress is one of the most versatile open source content management systems on the market. A publishing platform for building blogs and websites.

Introduction
WordPress Bitnami Chart bootstraps a  deployment on a  cluster using the  package manager.
It also packages MariaDB deployment for the database requirements of the WordPress application.

In this tutorial, we’ll use Helm for setting up WordPress on top of a Kubernetes cluster, in order to create a highly-available website.
In addition to leveraging the intrinsic scalability and high availability aspects of Kubernetes, this setup will help keeping WordPress secure by providing simplified upgrade and rollback workflows via Helm.

After completing the steps described in this tutorial, you will have a fully functional WordPress installation within a containerized cluster environment managed by Kubernetes.


#Objective of tutorial

In this tutorial,we are going to cover following topics:

- How to Install WordPress Bitnami Helm Chart and verify its successful installation.
- Verify status of pods and services. 
- Configurable parameters of the WordPress Bitnami Helm Chart and their default values.
-  How to access WordPress Console
- Uninstall WordPress Helm Chart and release resources






