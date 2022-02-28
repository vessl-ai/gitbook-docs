Module vessl.kernel_cluster
===========================

Functions
---------

    
`delete_cluster(cluster_id: int, **kwargs) ‑> object`
:   Delete custom cluster
    
    Keyword args:
        organization_name (str): override default organization

    
`list_cluster_nodes(cluster_id: int, **kwargs) ‑> List[openapi_client.models.response_kernel_cluster_node_info.ResponseKernelClusterNodeInfo]`
:   List custom cluster nodes
    
    Keyword args:
        organization_name (str): override default organization

    
`list_clusters(**kwargs) ‑> List[openapi_client.models.response_kernel_cluster_info.ResponseKernelClusterInfo]`
:   List clusters
    
    Keyword args:
        organization_name (str): override default organization

    
`read_cluster(cluster_name: str, **kwargs) ‑> openapi_client.models.response_kernel_cluster_info.ResponseKernelClusterInfo`
:   Read cluster
    
    Keyword args:
        organization_name (str): override default organization

    
`rename_cluster(cluster_id: int, new_cluster_name: str, **kwargs) ‑> openapi_client.models.response_kernel_cluster_info.ResponseKernelClusterInfo`
:   Rename custom cluster
    
    Keyword args:
        organization_name (str): override default organization