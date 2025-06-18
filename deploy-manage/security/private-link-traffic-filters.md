---
applies_to:
  deployment:
    ess: ga
  serverless: ga
navigation_title: "Add private connections"
products:
  - id: cloud-hosted
  - id: cloud-serverless
---

# Private connections

A private connection is a secure way for your {{ecloud}} deployments and projects to communicate with other cloud provider services over your cloud provider's private network. You can create a virtual private connection endpoint (VCPE) using your provider's private link service. You can also optionally filter traffic to your deployments and projects by creating ingress filters for your VCPE in {{ecloud}}.

Choose the relevant option for your cloud service provider:

| Cloud service provider | Service |
| --- | --- |
| AWS | [AWS PrivateLink](/deploy-manage/security/aws-privatelink-traffic-filters.md) |
| Azure | [Azure Private Link](/deploy-manage/security/azure-private-link-traffic-filters.md) |
| GCP | [GCP Private Service Connect](/deploy-manage/security/gcp-private-service-connect-traffic-filters.md) |

After you set up your private connection, you can [claim ownership of your VCPE ID](/deploy-manage/security/claim-traffic-filter-link-id-ownership-through-api.md) to prevent other organizations from using it.

To learn how private connection policies work, how they affect your deployment, and how they interact with [IP filter policies](ip-filtering-cloud.md), refer to [](/deploy-manage/security/network-security-policies.md).

:::{tip}
{{ech}} and {{serverless-full}} also support [IP filters](/deploy-manage/security/ip-filtering-cloud.md). You can apply both IP filters and private connections to a single {{ecloud}} resource.
:::
