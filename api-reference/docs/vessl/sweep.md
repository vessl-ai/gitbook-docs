Module vessl.sweep
==================

Functions
---------

    
`create_sweep(objective: openapi_client.models.orm_sweep_objective.OrmSweepObjective, max_experiment_count: int, parallel_experiment_count: int, max_failed_experiment_count: int, algorithm: str, parameters: List[openapi_client.models.orm_parameter.OrmParameter], cluster_name: str, start_command: str, kernel_resource_spec_name: str = None, processor_type: str = None, cpu_limit: float = None, memory_limit: float = None, gpu_type: str = None, gpu_limit: int = None, kernel_image_url: str = None, *, early_stopping_name: str = None, early_stopping_settings: List[Tuple[str, str]] = None, message: str = None, hyperparameters: List[Tuple[str, str]] = None, dataset_mounts: List[str] = None, git_ref_mounts: List[str] = None, git_diff_mount: str = None, archive_file_mount: str = None, root_volume_size: str = None, working_dir: str = None, output_dir: str = '/output/', **kwargs) ‑> openapi_client.models.response_sweep_info.ResponseSweepInfo`
:   Create sweep
    
    Args:
        parameters (List[Dict[str, Any]]):
            Element keys are 'name' (str), 'type' (str), and 'range' (dict).
            'range' keys are 'list' (list), 'min' (str), 'max' (str),
            and 'step' (str).
    
    Keyword args:
        organization_name (str): override default organization
        project_name (str): override default project
        use_git_diff (bool): run experiment with uncommitted changes
        use_git_diff_untracked (bool): run with untracked changed (only valid if `use_git_diff` is set)

    
`get_best_sweep_experiment(sweep_name: str, **kwargs) ‑> openapi_client.models.response_sweep_experiment_info.ResponseSweepExperimentInfo`
:   Read sweep and return the best experiment info
    
    Keyword args:
        organization_name (str): override default organization
        project_name (str): override default project

    
`list_sweep_logs(sweep_name: str, tail: int = 200, **kwargs) ‑> List[openapi_client.models.influxdb_sweep_log.InfluxdbSweepLog]`
:   List sweep logs
    
    Args:
        tail (int): number of lines to display from the end. Display all if -1.
    
    Keyword args:
        organization_name (str): override default organization
        project_name (str): override default project

    
`list_sweeps(**kwargs) ‑> List[openapi_client.models.response_sweep_list_response.ResponseSweepListResponse]`
:   List sweeps
    
    Keyword args:
        organization_name (str): override default organization
        project_name (str): override default project

    
`read_sweep(sweep_name: str, **kwargs) ‑> openapi_client.models.response_sweep_info.ResponseSweepInfo`
:   Read sweep
    
    Keyword args:
        organization_name (str): override default organization
        project_name (str): override default project

    
`terminate_sweep(sweep_name: str, **kwargs) ‑> openapi_client.models.response_sweep_info.ResponseSweepInfo`
:   Terminate sweep
    
    Keyword args:
        organization_name (str): override default organization
        project_name (str): override default project