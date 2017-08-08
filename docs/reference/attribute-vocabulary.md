---
title: Attribute Vocabulary
headline: 'Attribute Vocabulary'
sidenav: doc-side-reference-nav.html
bodyclass: docs
layout: docs
type: markdown
---

Attributes are a central concept used throughout Istio. You can find a description of what attributes are
and what they are used for [here]({{site.baseurl}}/docs/concepts/attributes.html).

A given Istio deployment has a fixed vocabulary of attributes that it understands. The specific vocabulary is
determined by the set of attribute producers being used in the deployment. The primary attribute producer in Istio
is Envoy, although Mixer and services can also introduce attributes.

## Standard Istio attribute vocabulary

The table below shows the set of canonical attributes and their respective types. Most Istio
deployments will have agents (Envoy or Mixer adapters) that produce these attributes.

| Name | Type | Description | Kubernetes Example |
|------|------|-------------|--------------------|
| source.ip         | ip_address | Client IP address. | 10.0.0.117 |
| source.service    | string | The fully-qualified domain name of the service that the client belongs to. | redis-master.default.svc.cluster.local |
| source.name       | string | The short name of the service that the client belongs to. | redis-master |
| source.namespace  | string | The namespace of the service that the client belongs to. | default |
| source.suffix     | string | The domain suffix of the source service fully-qualified domain name, excluding its name and namespace. | svc.cluster.local |
| source.uid        | string | Platform-specific unique identifier for the instance of the source service. | redis-master-2353460263-1ecey.default.pods.cluster.local |
| source.labels     | map[string, string] | Structured key-value pairs attached to the client instance. | version => v1 |
| source.user       | string | The user running the target application. | service-account@namespace.cluster.local |
| target.ip         | ip_address | Server IP address. | 10.0.0.104 |
| target.port       | int64 | Port accepting the requests on the server IP address. | 8080 |
| target.service    | string | The fully-qualified domain name of the service that the server belongs to. | my-svc.my-namespace.svc.cluster.local |
| target.name       | string | The short name of the service that the server belongs to. | my-svc |
| target.namespace  | string | The namespaces of the service that the server belongs to. | my-namespace |
| target.uid        | string | Platform-specific unique identifier for the instance of the target service. | my-svc-234499.my-namespace.pods.cluster.local |
| target.labels     | map[string, string] | Structured key-value pairs attached to the service instance. | version => v1 |
| target.user       | string | The user running the target application. | service-account@namespace.cluster.local |
| request.headers   | map[string, string] | HTTP request headers. | |
| request.id        | string | A unique ID with statistically low probability of collision for the HTTP request | |
| request.path      | string | HTTP URI path excluding the query string. | /ratings/v2/ |
| request.authority | string | HTTP authority header (host and port). | redis-master:3367 |
| request.method    | string | HTTP method. | GET |
| request.reason    | string | The system parameter for auditing reason. It is required for cloud audit logging and GIN logging | |
| request.referer   | string | The HTTP referer header. | |
| request.scheme    | string | URI Scheme of the request | |
| request.size      | int64 | Size of the request in bytes. For HTTP requests this is equivalent to the Content-Length header. | |
| request.time      | timestamp | The timestamp when the target receives the request. This should be equivalent to Firebase "now". | |
| request.user-agent | string | The HTTP User-Agent header. | |
| response.headers  | map | A map of HTTP headers attached to the response. | |
| response.size     | int64 | Size of the response body in bytes | |
| response.time     | timestamp | The timestamp when the target produced the response. | |
| response.duration | duration | The amount of time the response took to generate. | |
| response.code     | int64 | The response's HTTP status code | |
