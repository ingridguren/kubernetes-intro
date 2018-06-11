# Installation and setup 

## Kubernetes cluster
We need a cluster in order to continue with this workshop. There are two alternatives here. We recommend the first alternative. With the second you must skip the tasks to create build triggers and apply changes to the application code.
1. Set up your own cluster on Google Cloud Platform. In order to do this, you need to register your credit card, but you will not be charged anything for this workshop. To do this, follow the steps in [./tasks/gcp-setup.yaml](./tasks/gcp-setup.yaml)
2. The second alternative is to use a service account to authenticate against a cluster we have already created. To do this, follow the steps in [./tasks/service-account-setup.yaml](./tasks/service-account-setup.yaml)

## Install the Kubernetes command-line tool
1. To operate our cluster, we will use the Kubernetes command line tool, kubectl:
```
   gcloud components install kubectl
```

The cloud SDK installs the tool for you. This tool is not Google Cloud specific, but is used to operate Kubernetes clusters regardless of where they are hosted.

2. You can see if your cluster is created by this command:
    ```
   gcloud container clusters list
   ```

If the status of your cluster is `RUNNING`, you are good to go.

3. The next step is to make sure that the Kubernetes command line tool is authenticated against our new cluster. This is easily done by this neat gcloud command:
    ```
   gcloud container clusters get-credentials cv-cluster
   ```

What this does is to write credentials to the file `~/.kube/config`. You can take a look at that file too see what is written to it.

If you want bash autocompletion for kubectl, follow [these steps](https://kubernetes.io/docs/tasks/tools/install-kubectl/#enabling-shell-autocompletion).

## Describe components of the cluster
Now that we are authenticated, we can look at the components in our cluster by using the kubectl command.

1. Remember how Kubernetes consists of nodes? List them by this command:
    ```
   kubectl get nodes
   ```

2. If you want you can get more details about them by describing one of them:
    ```
   kubectl describe nodes <INSERT_NODE_NAME>
   ```

3. We also have different namespaces:
    ```
   kubectl get namespace
   ```

This should list three namespaces. `kube-system`, `kube-public` and `default`. The namespace `default`is where we will deploy our applications. `kube-system` is used by Kubernetes, `kube-public` is for resources that does not need authentication and `default` is, as the name says, the default namespace for resources. You can create your own namespaces, e.g. for test and prod.