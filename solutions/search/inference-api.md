---
mapped_urls:
  - https://www.elastic.co/guide/en/kibana/current/inference-endpoints.html

navigation_title: Inference integrations
---

# Integrate with third-party services

{{es}} provides a machine learning [inference API](https://www.elastic.co/docs/api/doc/elasticsearch/v8/group/endpoint-inference) to create and manage inference endpoints to integrate with machine learning models provide by popular third-party services like Amazon Bedrock, Anthropic, Azure AI Studio, Cohere, Google AI, Mistral, OpenAI, Hugging Face, and more.

Learn how to integrate with specific services in the subpages of this section.

## Managing inference endpoints [inference-endpoints]

Inference endpoints can be managed using both the {{es}} [REST API](https://www.elastic.co/docs/api/doc/elasticsearch) and the {{kib}} UI **Inference endpoints** page.

### Inference endpoints UI

In {{kib}}, the **Inference endpoints** page provides a graphical interface for managing inference endpoints.

:::{image} ../../images/kibana-inference-endpoints-ui.png
:alt: Inference endpoints UI
:class: screenshot
:::

Available actions:

* Add new endpoint
* View endpoint details
* Copy the inference endpoint ID
* Delete endpoints

## Add new inference endpoint

To add a new interference endpoint using the UI:

1. Select the **Add endpoint** button.
1. Select a service from the drop down menu.
1. Provide the required configuration details.
1. Select **Save** to create the endpoint.