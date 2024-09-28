# Setting Up KubeReport with Helm

This demo will guide you through the process of setting up KubeReport using Helm.

## Prerequisites

Before starting, ensure you have the following installed:

- **Docker**: Ensure Docker is installed and running on your machine.
- **Helm**: Install Helm and verify that it is correctly set up.
- **Kubernetes Cluster**: Ensure you have a running Kubernetes cluster.

## Helm Chart Installation

1. **Add the KubeReport Helm Repository**:
    ```bash
    helm repo add kubereport https://kubesuiteorg.github.io/kubereport-helm-chart
    ```

2. **Update Your Helm Repositories**:
    ```bash
    helm repo update
    ```

3. **Install KubeReport**:
    You can customize the installation using your own `values.yaml` file:
    ```bash
    helm install kubereport kubereport/kubereport -f values.yaml
    ```

    ### Configuration in `values.yaml`
    You can customize the `values.yaml` file for your deployment. Below is a sample configuration:

    ```yaml
    # Reporting Configuration [Default values]
    report:
      type: "detailed"
      schedulable:
        enabled: true
        schedule: "* * * * *"

    # SMTP Configuration
    smtp:
      enabled: false
      server: "smtp.gmail.com"
      port: "587"
      useTLS: "true"
      recipient: "recipient@example.com"
      sender: "sender@gmail.com"
      password: "XXXXXXXXXX"
      subject: "Kubernetes cluster report"
      body: |
        Hi,

        The latest Kubernetes cluster report has been generated and is attached for your reference.

        Thanks
        KubeReport,

    # Persistent Volume Configuration
    persistence:
      enabled: false
      storageClass: ""
      capacity: "100Mi"
      request: "100Mi"
      accessModes: 
        - ReadWriteOnce
      pvpolicy: "Retain"
      secretName: azure-secret
      secretValues:
        azurestorageaccountname: XXXXXXXXXX
        azurestorageaccountkey: XXXXXXXXXX
      provider:
        azureFile:
          secretName: azure-secret
          shareName: XXXXXXXXXX
          readOnly: false
        mountOptions:
          - dir_mode=0777
          - file_mode=0777
          - uid=1000
          - gid=1000
          - mfsymlinks
          - nobrl
    ```

4. **Verify the Installation**:
    Check that the KubeReport pods are running:
    ```bash
    kubectl get pods -n kubereport
    ```

    - **Gmail App Password**: Generate an app password from your Google account [here](https://myaccount.google.com/apppasswords).
    - **Outlook App Password**: Generate an app password from your Outlook account [here](https://account.live.com/proofs/AppPassword).

Now you're all set to use `KubeReport` to generate and manage your Kubernetes cluster reports!
