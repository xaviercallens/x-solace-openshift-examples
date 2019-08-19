# solace-openshift-examples

## Synopsis

This project provides a series of OpenShift Templates that are samples for deploying Solace PubSub+ brokers and Solace Applications into an
OpenShift Cluster.

Detailed notes can be found in the Documents directory. You will need to download the document be be able to read the entire document.

The templates are a series of Solace-related OpenShift templates with increasing capabilities; each template is based in the previous template and provides more functionality and/or features than the previous. These templates require at least PubSub+ version 9.3.0 to operate since they are expected to operate in the most secure OpenShift environment available.

Below is a brief description for each of the sample Solace/OpenShift Templates (more details can be found in the Documents folder):

**sol-single-ps+-persist-pod.yml** - This is the most basic way to deploy a Solace PubSub+ singleton broker as a simple OpenShift Pod. All the required ClusterIP and NodePort services are also configured for internal and external access to the broker in OpenShift. The PubSub+ docker image is loaded from the public Docker repository.

**sol-single-ps+-persist-pod-reg-img.yml** - This template is similar to the previous template, except that it make use of a PubSub+ image that was loaded into the project's OpenShift local repository. This is required for licensed Enterprise PubSub+ brokers. Details for loading the docker image into the project repository are described in the enclosed document.

**sol-ha-ps+-persist-pod.yml** - The previous template still only deployed a single PubSub+ broker.  With this template a full HA cluster is deployed from the single template. The images are installed as simple Pods. The template also includes a defined Load Balance Service for access to the non-monitoring Pods. Only minimal configuration is required once the PubSub+ brokers are installed. 

**sol-ha-ps+-persist-deploymentconfig-configmap.yml** - Much like the previous template, an HA cluster is deployed. However, rather than simple pods, an OpenShift deployment configuration is utilized. As a result a controller process will ensure if any Solace Pod is stopped or the Node the Pod is running on stops, the Pod will be restarted on another node. Deployment Configurations also allow the mounting of ConfigMaps, which is also included with this template. The ConfigMap is used to provide scripts that will automatically provide the final config-sync configuration that was required to be performed manually with the previous template. This template also makes use of OpenShift Secrets that can be used to obfuscate the admin username and passowrd for the Solace PubSub+ brokers.

**sol-ha-ps+-persist-statefulset-configmap.yml** - Rather than using OpenShift Deployment Configuration controllers, this template makes use of StatefulSets. Unlike the previous template, the required scripts in the ConfigMap are defined in the same template. A more dynamic Load Balancing is also set up in this template. This template is very similar to the Solace Quick Start for OpenShift.

**sample-aggregator-app.yml** - A template that deploys both a PubSub+ broker and two Java applications. The applications are deployed from source code that is stored in GitHub using the OpenShift Source-to-Image (S2I) capability. The deployed applications communicate via the broker and the worker application can be used to show linear scaling where increasing the number of running worker Pods increases the throughput performance.  

## Contributing

Please read [CONTRIBUTING.md](CONTRIBUTING.md) for details on our code of conduct, and the process for submitting pull requests to us.

## Authors

See the list of [contributors](../../graphs/contributors) who participated in this project.

## License

This project is licensed under the Apache License, Version 2.0. - See the [LICENSE](LICENSE) file for details.

## Resources

For more information about Solace technology in general please visit these resources:

- The Solace Developer Portal website at: http://dev.solace.com
- Understanding [Solace technology.](http://dev.solace.com/tech/)
- Ask the [Solace community](http://dev.solace.com/community/).