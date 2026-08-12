# gitops-install-acs
Deploy Red Hat Advanced Cluster Security (ACS) across ACM hub and managed clusters using OpenShift GitOps / ArgoCD.

## Overview

This repo uses an App of Apps pattern. When applied to the hub cluster, it creates an ArgoCD Application that uses the ACM PolicyGenerator Config Management Plugin to render and apply the ACS policies from `acm-install-acs`.

## Prerequisites

- OpenShift GitOps (ArgoCD) installed with the `policy-generator` CMP configured
- Red Hat Advanced Cluster Management 2.6+

## Deployment

This repo is deployed by the `apps_install_acs` Ansible role in `acm-global-hub-automation`, which creates an ArgoCD Application pointing at `acs/` in this repo.

To apply manually:

```bash
oc apply -f acs/01-acs-policy-application.yaml
```

ArgoCD will pick up the child Application and begin syncing ACS policies from `acm-install-acs` using the `policy-generator` plugin.
