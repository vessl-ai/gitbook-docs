Module vessl.workspace
======================

Functions
---------

    
`backup_workspace() ‑> None`
:   Backup the home directory of the workspace
    
    Should only be called inside a workspace.

    
`connect_workspace_ssh(private_key_path: str, **kwargs) ‑> None`
:   Connect to a running workspace via SSH
    
    Keyword args:
        organization_name (str): override default organization

    
`create_workspace(name: str, cluster_name: str, cluster_node_names: List[str] = None, kernel_resource_spec_name: str = None, processor_type: str = None, cpu_limit: float = None, memory_limit: str = None, gpu_type: str = None, gpu_limit: int = None, kernel_image_url: str = None, max_hours: int = 24, dataset_mounts: List[str] = None, local_files: List[str] = None, root_volume_size: str = '100Gi', ports: List[Dict[str, Any]] = None, init_script: str = None, **kwargs) ‑> openapi_client.models.response_workspace_detail.ResponseWorkspaceDetail`
:   Create workspace
    
    Args:
        ports (List[Dict[str, Any]]):
            Element keys are 'expose_type' (str), 'port' (int), and 'name' (dict).
    
    Keyword args:
        organization_name (str): override default organization

    
`list_workspace_logs(workspace_id: int, tail: int = 200, **kwargs) ‑> List[openapi_client.models.influxdb_workload_log.InfluxdbWorkloadLog]`
:   List experiment logs
    
    Args:
        tail (int): number of lines to display from the end. Display all if -1.
    
    Keyword args:
        organization_name (str): override default organization

    
`list_workspaces(cluster_id: int = None, statuses: List[str] = None, mine: bool = True, **kwargs) ‑> List[openapi_client.models.response_workspace_list.ResponseWorkspaceList]`
:   List workspaces
    
    Keyword args:
        organization_name (str): override default organization

    
`read_workspace(workspace_id: int, **kwargs) ‑> openapi_client.models.response_workspace_detail.ResponseWorkspaceDetail`
:   Read workspace
    
    Keyword args:
        organization_name (str): override default organization

    
`restore_workspace(workspace_id: int = None) ‑> None`
:   Restore the home directory from the previous backup
    
    Should only be called inside a workspace.

    
`start_workspace(workspace_id: int, **kwargs) ‑> openapi_client.models.response_workspace_detail.ResponseWorkspaceDetail`
:   

    
`stop_workspace(workspace_id: int, **kwargs) ‑> openapi_client.models.response_workspace_detail.ResponseWorkspaceDetail`
:   

    
`terminate_workspace(workspace_id: int, **kwargs) ‑> openapi_client.models.response_workspace_detail.ResponseWorkspaceDetail`
:   

    
`update_vscode_remote_ssh(private_key_path: str) ‑> None`
:   Update .ssh/config file for VSCode Remote-SSH plugin