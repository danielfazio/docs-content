---
navigation_title: How policies work in Cloud
applies_to:
  deployment:
    ess: ga
  serverless: ga
---

# Network security policies in {{ecloud}}

By default, in {{ech}} and {{serverless-full}}, all your deployments are accessible over the public internet.

Network security policies are created at the organization level, and then are associated with one or more resources, such as a deployment or project, to take effect. After you associate at least one policy with a resource, traffic that does not match the policy or any other policy associated with the resource is denied.

Policies apply to external traffic only. Internal traffic is managed by the deployment or project. For example, in {{ech}}, {{kib}} can connect to {{es}}, as well as internal services which manage the deployment, Other deployments can’t connect to deployments protected by network security policies.

Policies operate on the proxy. Requests rejected by the policies are not forwarded to the resource. The proxy responds to the client with `403 Forbidden`.

## Logic

- You can assign multiple policies to a single deployment or project. The policies can be of different types if applicable. In case of multiple policies, traffic can match any associated policy to be forwarded to the resource. If none of the policies match, the request is rejected with `403 Forbidden`.
- Policies, when associated with a deployment or project, will apply to all endpoints, such as {{es}}, {{kib}}, APM Server, and others.
- Any policy assigned to a deployment overrides the default behavior of *allow all access over the public internet endpoint*. The implication is that if you make a mistake putting in the traffic source (for example, if you specified the wrong IP address) the deployment will be effectively locked down to any of your traffic. You can use the UI to adjust or remove the policies.
- You can [mark a policy as default](#default-network-security-policies). Default policies are automatically attached to all new resources of the matching resource type that you create in its region.

## Restrictions

- You can have a maximum of 1024 policies per organization and 128 sources in each policy.
- Policies must be created for a specific resource type. If you want to associate a policy to both hosted deployments and Serverless projects, then you have to create the same policy for each resource types.
- Policies are bound to a single region, and can be assigned only to deployments or projects in the same region. If you want to associate a policy with resources in multiple regions, then you have to create the same policy in all the regions you want to apply it to.
- Domain-based filtering rules are not allowed for network security policies, because the original IP is hidden behind the proxy. Only IP-based filtering rules are allowed.

## Default network security policies

You can mark a policy as default. Default policies are automatically attached to all new resources of the matching resource type that you create in its region.

You can detach default policies from resources after they are created. Default policies are not automatically attached to existing resources.

### Apply policies to new resources by default

To automatically apply a network security policy to new resources by default new deployments or projects in your organization:

1. Log in to the [{{ecloud}} Console](https://cloud.elastic.co?page=docs&placement=docs-body).
2. From any deployment or project on the home page, select **Manage**.
3. Under the **Features** tab, open the **Network security** page.
4. Select **Create** to create a new policy, or select **Edit** to open an existing policy.
5. Under **Apply to future resources by default**, select **Include by default**.

### Identify default policies

To identify which network security policies are automatically applied to new deployments or projects in your organization:

1. Log in to the [{{ecloud}} Console](https://cloud.elastic.co?page=docs&placement=docs-body).
2. From any deployment or project on the home page, select **Manage**.
3. Under the **Features** tab, open the **Network security** page.
4. Select each of the policies. **Include by default** is checked when a policy is automatically applied to all new deployments or projects in its region.
  
## Review the policies associated with a resource

To identify the network security policies that are applied to your deployment or project:

::::{tab-set}
:::{tab-item} Serverless
1. Log in to the [{{ecloud}} Console](https://cloud.elastic.co?page=docs&placement=docs-body).
2. On the **Serverless projects** page, select your project.
3. Select the **Network security** tab on the left-hand side menu bar.

Network security policies are listed on the page. From this page, you can view and remove existing policies and attach new policies.

:::
:::{tab-item} Hosted
1. Log in to the [{{ecloud}} Console](https://cloud.elastic.co?page=docs&placement=docs-body).
2. On the **Hosted deployments** page, select your deployment.
3. Select the **Network security** tab on the left-hand side menu bar.
4. Select the **Security** tab on the left-hand side menu bar.

Network security policies are listed under **Network security**. From this section, you can view and remove existing policies and attach new policies.
:::
::::

## View rejected requests

Requests rejected by a network security policy have the status code `403 Forbidden` and one of the following in the response body:

```json
{"ok":false,"message":"Forbidden"}
```

```json
{"ok":false,"message":"Forbidden due to traffic filtering. Please see the Elastic documentation on Traffic Filtering for more information."}
```

Additionally, network security policy rejections are logged in ECE proxy logs as `status_reason: BLOCKED_BY_IP_FILTER`. Proxy logs also provide client IP in `client_ip` field.