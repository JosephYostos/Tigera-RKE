# Calico workshop on RKE

<img src="img/calico-on-eks.png" alt="Calico on EKS" width="30%"/>

## Workshop objectives

The intent of this workshop is to educate any person working with RKE cluster in one way or another about Calico features and how to use them. While there are many capabilities that Calico provides, this workshop focuses on a subset of those that are used most often by different types of technical users.

## Use cases

In this workshop we are going to focus on these main use cases:

- **East-West security**, leveraging zero-trust security approach.
- **Egress access controls**, using DNS policy to access external resources by their fully qualified domain names (FQDN).
- **Host micro-segmentation**, leveraging Calico policies to protect host ports and host based services.
- **Observability**, exploring various logs and application level metrics collected by Calico.
- **Compliance**, providing proof of security compliance.
- **Security alerts**, configuring alerts to notify security and operations teams of any security incidents or anomalous behaviors.
- **Dynamic packet capture**, capturing full packet payload on demand for further forensic analysis.

## Join the Slack Channel

[Calico User Group Slack](https://slack.projectcalico.org/) is a great resource to ask any questions about Calico. If you are not a part of this Slack group yet, we highly recommend [joining it](https://slack.projectcalico.org/) to participate in discussions or ask questions. 


## Modules


- [Module 1: Joining RKE cluster to Calico Cloud](modules/joining-RKE-to-calico-cloud.md)
- [Module 2: Configuring demo applications](modules/configuring-demo-apps.md)
- [Module 3: Using security controls](modules/using-security-controls.md)
- [Module 4: Using egress access controls](modules/using-egress-access-controls.md)
- [Module 5: Securing RKE hosts](modules/securing-heps.md)
- [Module 6: Using observability tools](modules/using-observability-tools.md)
- [Module 7: Using compliance reports](modules/using-compliance-reports.md)
- [Module 8: Using alerts](modules/using-alerts.md)
- [Module 9: Dynamic packet capture](modules/dynamic-packet-capture.md)

