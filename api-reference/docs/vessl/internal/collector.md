Module vessl.internal.collector
===============================

Classes
-------

`Collector()`
:   Helper class that provides a standard way to create an ABC using
    inheritance.

    ### Ancestors (in MRO)

    * abc.ABC

    ### Descendants

    * vessl.internal.collector.IOCollector
    * vessl.internal.collector.K8sCollector
    * vessl.internal.collector.SystemMetricCollector
    * vessl.internal.collector.UserMetricCollector

    ### Class variables

    `DROP_THRESHOLD`
    :

    ### Methods

    `add(self, entries: List[openapi_client.models.experiment_metric_entry.ExperimentMetricEntry])`
    :

    `collect(self)`
    :

    `start(self)`
    :

    `stop(self)`
    :

    `truncate(self, idx)`
    :

`IOCollector()`
:   Helper class that provides a standard way to create an ABC using
    inheritance.

    ### Ancestors (in MRO)

    * vessl.internal.collector.Collector
    * abc.ABC

    ### Methods

    `create_callback(self, io_name)`
    :

    `create_write_hook(self, orig_write, io_name)`
    :

    `start(self)`
    :

    `stop(self)`
    :

`K8sCollector()`
:   Helper class that provides a standard way to create an ABC using
    inheritance.

    ### Ancestors (in MRO)

    * vessl.internal.collector.Collector
    * abc.ABC

    ### Methods

    `start(self)`
    :

    `stop(self)`
    :

`SystemMetricCollector(gpu_count: int)`
:   Helper class that provides a standard way to create an ABC using
    inheritance.

    ### Ancestors (in MRO)

    * vessl.internal.collector.Collector
    * abc.ABC

    ### Methods

    `start(self)`
    :

    `stop(self)`
    :

`UserMetricCollector()`
:   Helper class that provides a standard way to create an ABC using
    inheritance.

    ### Ancestors (in MRO)

    * vessl.internal.collector.Collector
    * abc.ABC

    ### Methods

    `build_media_payload(self, payload: Dict[str, Any], ts: float)`
    :

    `build_metric_payload(self, payload: Dict[str, Any], ts: float)`
    :

    `handle_step(self, step: Optional[int])`
    :

    `log_media(self, payloads: List[openapi_client.models.experiment_metric_entry.ExperimentMetricEntry]) ‑> int`
    :

    `log_metrics(self, payloads: List[openapi_client.models.experiment_metric_entry.ExperimentMetricEntry]) ‑> int`
    :

    `start(self)`
    :

    `stop(self)`
    :