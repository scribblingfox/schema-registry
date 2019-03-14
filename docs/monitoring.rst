.. _schemaregistry_monitoring:

Monitoring |sr|
---------------

|sr| reports a variety of metrics through JMX. View the available metrics by using jconsole to browse JMX MBeans. You can also use the ``metrics.reporters`` parameter to configure |sr| to report additional metrics. For more information about configuring |sr|, see [TOPIC-NAME-TK](URL-PATH-TO-RELATED-TOPIC-HERE).

|sr| has two types of metrics: 
* Global metrics help you monitor the overall health of
the service. 
* Per-endpoint metrics monitor each API endpoint request method. 

These two metrics help you understand how the proxy is functioning and identify specific performance problems.

Global Metrics
~~~~~~~~~~~~~~

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
MBean: kafka.schema.registry:type=jetty-metrics
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

``connections-active``
    Total number of active TCP connections.

``connections-accepted-rate`` (deprecated since 2.0)
    * In 1.x: The average rate per second of accepted TCP connections.
    * In 2.x: Same behavior as ``connections-opened-rate``.

``connections-opened-rate``
    The average rate per second that TCP connections open.

``connections-closed-rate``
    The average rate per second that TCP connections close.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
MBean: kafka.schema.registry:type=master-slave-role
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

``master-slave-role``
    The current role of this |sr| instance. A value of 1 indicates this instance is
    the master, 0 indicates it is a slave.


Per-Endpoint Metrics
~~~~~~~~~~~~~~~~~~~~

The following metrics are available for each endpoint request method. Metrics for all
requests are also aggregated into a global instance. Each metric has a corresponding global instance. You can differentiate between global and individual instances because global instances have no prefix in their name.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
MBean: kafka.schema.registry:type=jersey-metrics
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

``<endpoint>.request-byte-rate``
    The number of bytes per second for incoming requests.

``<endpoint>.request-error-rate``
    The average number of requests per second that resulted in HTTP error responses.

``<endpoint>.request-latency-avg``
    The average request latency in millseconds.

``<endpoint>.request-latency-max``
    The maximum request latency in millseconds.

``<endpoint>.request-rate``
    The average number of HTTP requests per second.

``<endpoint>.request-size-avg``
    The average request size in bytes.

``<endpoint>.request-size-max``
    The maximum request size in bytes.

``<endpoint>.response-byte-rate``
    The number of bytes per second for outgoing responses.

``<endpoint>.response-rate``
    The average number of HTTP responses per second.

``<endpoint>.response-size-avg``
    The average response size in bytes.

``<endpoint>.response-size-max``
    The maximum response size in bytes.


Endpoints
~~~~~~~~~

The following is a list of all the API endpoint methods. To create a full metric name, prefix a per-endpoint metric name with
one of these values. 

For example, to find the rate of ``GET /brokers`` API calls, combine the
endpoint name ``brokers.list`` with the metric name ``request-rate`` to get
``brokers.list.request-rate``.

========================================== =======================================================
``compatibility.subjects.versions.verify`` ``POST /compatibility/subjects/{subject}/versions/{version}``
``schemas.ids.get-schema``                 ``GET /schemas/ids/{id}``
``subjects.get-schema``                    ``POST /subjects/{subject}``
``subjects.list``                          ``GET /subjects``
``subjects.versions.get-schema``           ``GET /subjects/{subject}/versions/{version}``
``subjects.versions.get-schema.only``      ``GET /subjects/{subject}/versions/{version}/schema``
``subjects.versions.list``                 ``GET /subjects/{subject}/versions``
``subjects.versions.register``             ``POST /subjects/{subject}/versions``
========================================== =======================================================
