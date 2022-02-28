Module vessl.experiment
=======================

Functions
---------

    
`create_experiment(cluster_name: str, start_command: str, kernel_resource_spec_name: str = None, processor_type: str = None, cpu_limit: float = None, memory_limit: str = None, gpu_type: str = None, gpu_limit: int = None, kernel_image_url: str = None, *, message: str = None, termination_protection: bool = False, hyperparameters: List[str] = None, dataset_mounts: List[str] = None, model_mounts: List[str] = None, git_ref_mounts: List[str] = None, git_diff_mount: str = None, local_files: List[str] = None, upload_local_git_diff: bool = None, archive_file_mount: str = None, root_volume_size: str = None, working_dir: str = None, output_dir: str = '/output/', worker_count: int = 1, framework_type: str = None, **kwargs) ‑> openapi_client.models.response_experiment_info.ResponseExperimentInfo`
:   Create experiment
    
    Keyword args:
        organization_name (str): override default organization
        project_name (str): override default project
        git_branch (str): override current git branch
        git_ref (str): override current git commit
        use_git_diff (bool): run experiment with uncommitted changes
        use_git_diff_untracked (bool): run with untracked changed (only valid if `use_git_diff` is set)

    
`create_local_experiment(message: str = None, hyperparameters: dict = None, **kwargs)`
:   

    
`download_experiment_output_files(experiment_name: str, dest_path: str = '/Users/intaeryoo/Documents/savvihub/github/vessl-python-sdk/output', worker_number: int = 0, **kwargs) ‑> None`
:   Download experiment output files
    
    Keyword args:
        organization_name (str): override default organization
        project_name (str): override default project

    
`list_experiment_logs(experiment_name: str, tail: int = 200, worker_number: int = 0, after: int = 0, **kwargs) ‑> List[openapi_client.models.influxdb_workload_log.InfluxdbWorkloadLog]`
:   List experiment logs
    
    Args:
        experiment_name (str): experiment name or number
        tail (int): number of lines to display from the end. Display all if -1.
        worker_number (int): override default worker number
    
    Keyword args:
        organization_name (str): override default organization
        project_name (str): override default project

    
`list_experiment_output_files(experiment_name: str, need_download_url: bool = False, recursive: bool = True, worker_number: int = 0, **kwargs) ‑> List[openapi_client.models.response_file_metadata.ResponseFileMetadata]`
:   List experiment output files
    
    Keyword args:
        organization_name (str): override default organization
        project_name (str): override default project

    
`list_experiments(statuses: List[str] = None, **kwargs) ‑> List[openapi_client.models.response_experiment_list_response.ResponseExperimentListResponse]`
:   List experiments
    
    Keyword args:
        organization_name (str): override default organization
        project_name (str): override default project

    
`read_experiment(experiment_name_or_number: str, **kwargs) ‑> openapi_client.models.response_experiment_info.ResponseExperimentInfo`
:   Read experiment
    
    Keyword args:
        organization_name (str): override default organization
        project_name (str): override default project

    
`read_experiment_by_id(experiment_id: int, **kwargs) ‑> openapi_client.models.response_experiment_info.ResponseExperimentInfo`
:   

    
`terminate_experiment(experiment_name: str, **kwargs) ‑> openapi_client.models.response_experiment_info.ResponseExperimentInfo`
:   

    
`upload_experiment_output_files(experiment_name: str, path: str, **kwargs)`
: