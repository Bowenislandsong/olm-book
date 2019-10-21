# How do I install OLM?

The OLM is installable on Kubernetes clusters. It is already installed and available by default on 4.x OpenShift 
clusters. For the following instructions to work, you must have a Kubernetes cluster running and the `kubectl` 
command-line tool is able to find the information it needs to communicate with the API server of that cluster. For more 
information about configuring `kubectl`, please visit 
[here](https://kubernetes.io/docs/concepts/configuration/organize-cluster-access-kubeconfig/).

## Install Released OLM
For installing release versions of OLM, for example version 0.12.0, you can use the following command:
```bash
export olm_release=0.12.0
kubectl apply -f https://github.com/operator-framework/operator-lifecycle-manager/releases/download/${olm_release}/crds.yaml
kubectl apply -f https://github.com/operator-framework/operator-lifecycle-manager/releases/download/${olm_release}/olm.yaml
```

For detailed install instructions of individual releases, please visit the 
[latest release on GitHub](https://github.com/operator-framework/operator-lifecycle-manager/releases).

## Install From Git Repository

You can install OLM from the master branch of the 
[operator-framework/operator-lifecycle-manager](https://github.com/operator-framework/operator-lifecycle-manager/) repository with 
the following: 

```bash
git clone https://github.com/operator-framework/operator-lifecycle-manager.git
cd operator-lifecycle-manager
kubectl create -f deploy/upstream/quickstart/crds.yaml
kubectl create -f deploy/upstream/quickstart/olm.yaml
```

## Install locally with minikube

To install OLM locally on a minikube cluster, you need to spawn a 1.14.2 minikube cluster and then follow the previous 
instructions installing from OLM releases or Git Repositories:
```bash
minikube start  --kubernetes-version=1.14.2 
```

## Verify OLM Install

You can verify the necessary Custom Resource Definitions are created from applying the `crds.yaml` file with ```kubectl
 get crd``` and 
expect the 
following output:
```bash
NAME                                          CREATED AT
catalogsources.operators.coreos.com           2019-10-21T18:15:27Z
clusterserviceversions.operators.coreos.com   2019-10-21T18:15:27Z
installplans.operators.coreos.com             2019-10-21T18:15:27Z
operatorgroups.operators.coreos.com           2019-10-21T18:15:27Z
subscriptions.operators.coreos.com            2019-10-21T18:15:27Z
```
You can also visualize OLM deployments from applying `olm.yaml` file with ```kubectl get deploy -n olm``` and expect 
the 
following:
```bash
NAME               READY   UP-TO-DATE   AVAILABLE   AGE
catalog-operator   1/1     1            1           5m52s
olm-operator       1/1     1            1           5m52s
packageserver      2/2     2            2           5m43s
```