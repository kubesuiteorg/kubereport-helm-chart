# KubeReport Helm Chart

This repository contains the Helm chart for deploying KubeReport to a Kubernetes cluster. KubeReport simplifies the management of Kubernetes clusters by generating comprehensive reports that can be scheduled, sent via email, and stored in the cloud for easy access and archival.

## Features

- **Scheduled Reporting**: Automatically generate and send reports at specified intervals.
- **Customizable SMTP Settings**: Configure email settings to send reports directly to recipients.
- **Persistent Storage**: Optionally store generated reports in cloud storage.
- **Lightweight Deployment**: Easily deploy KubeReport using Helm.

## Installation

To install the chart, use the following command:

```bash
helm repo add kubereport https://kubesuiteorg.github.io/kubereport-helm-chart
helm repo update
helm install kubereport kubereport/kubereport
```

Verify the Installation

```bash
kubectl get pods -n kubereport
```

## Configuration Parameters

### Report Configuration

| Parameter                    | Description                                                            | Default Value             |
|------------------------------|------------------------------------------------------------------------|---------------------------|
| `report.type`                | Type of report to generate (e.g., detailed, general)                  | `detailed`                |
| `report.schedulable.enabled` | Enable or disable scheduled reporting                                   | `true`                    |
| `report.schedulable.schedule`| Cron schedule for generating reports (in cron format)                 | `* * * * *`               |

### SMTP Configuration

| Parameter                     | Description                                                            | Default Value              |
|-------------------------------|------------------------------------------------------------------------|----------------------------|
| `smtp.enabled`                | Enable or disable SMTP configuration                                   | `false`                    |
| `smtp.server`                 | SMTP server address                                                   | `smtp.gmail.com`          |
| `smtp.port`                   | Port number for SMTP                                                  | `587`                      |
| `smtp.useTLS`                 | Enable or disable TLS for SMTP                                        | `true`                     |
| `smtp.recipient`              | Recipient email address for sending reports                           | `example@example.com`     |
| `smtp.sender`                 | Sender email address                                                  | `example@gmail.com`  |
| `smtp.password`               | SMTP server password (should be stored in a secret in production)    | `sdaridfdrnyzrtlt`        |
| `smtp.subject`                | Subject line for the report email                                     | `Kubernetes Cluster Report`|
| `smtp.body`                   | Body of the report email                                             | (default body content)    |

## Persistent Volume Configuration

| Parameter                          | Description                                                                          | Default Value                 |
|------------------------------------|--------------------------------------------------------------------------------------|-------------------------------|
| `persistence.enabled`              | Enable or disable persistent volume storage                                          | `false`                       |
| `persistence.storageClass`         | Storage class for the persistent volume                                              | `""` (default storage class)  |
| `persistence.capacity`             | Total storage capacity for the persistent volume                                     | `100Mi`                       |
| `persistence.request`              | Requested storage capacity for the persistent volume                                 | `100Mi`                       |
| `persistence.accessModes`          | Access modes for the persistent volume (e.g., ReadWriteOnce)                       | `ReadWriteOnce`               |
| `persistence.pvpolicy`             | Policy for persistent volume (e.g., Retain, Delete)                                 | `Retain`                      |
| `persistence.secretName`           | Name of the secret containing sensitive data                                         | `azure-secret`                |
| `persistence.secretValues`         | Values stored in the secret, such as Azure storage account details                  | (obfuscated values)           |
| `persistence.provider`             | Cloud provider configuration for the persistent volume                               |                               |

## Demo

You can view the demo in the [test](test/README.md).

## Your Support Matters

KubeReport is a community-driven open-source project, maintained with dedication and effort. We are committed to keeping it free for everyone!

If KubeReport enhances your Kubernetes experience, please consider supporting us! Your [sponsorship](https://buymeacoffee.com/sachinran) will help us continue development and deliver valuable updates. Every contribution counts, and we greatly appreciate your support!

## Contribution Guidelines

* **File an Issue or Suggestions**
* **Comment Your Code**
* **Attach Tested Output**

## Community & Support

Want to discuss KubeReport features with other users or show your support for this tool?

- **Invite**: Get your [KubeReport Slack Invite](https://join.slack.com/t/newworkspace-lnq1467/shared_invite/zt-2rh7j3whw-We_16ybaeK5tNjRXGenX_Q).
- **Slack Channel**: Join the conversation on [KubeReport Slack](https://kubesuite.slack.com/archives/C07PPLEUR7B).

You can also connect with us on [LinkedIn](https://www.linkedin.com/company/kubesuite/) to stay updated and engage with the community.