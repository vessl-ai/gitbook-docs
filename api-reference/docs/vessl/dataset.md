Module vessl.dataset
====================

Functions
---------

    
`copy_dataset_volume_file(dataset_name: str, source_path: str, dest_path: str, recursive: bool = False, **kwargs) ‑> None`
:   Copy files within a same dataset
    
    Keyword args:
        organization_name (str): override default organization

    
`create_dataset(dataset_name: str, description: str = None, is_version_enabled: bool = False, is_public: bool = False, external_path: str = None, aws_role_arn: str = None, version_path: str = None, **kwargs) ‑> openapi_client.models.response_dataset_info_detail.ResponseDatasetInfoDetail`
:   Create dataset
    
    Keyword args:
        organization_name (str): override default organization

    
`delete_dataset_volume_file(dataset_name: str, path: str, recursive: bool = False, **kwargs) ‑> List[openapi_client.models.response_file_metadata.ResponseFileMetadata]`
:   Delete dataset volume file
    
    Keyword args:
        organization_name (str): override default organization

    
`download_dataset_volume_file(dataset_name: str, source_path: str, dest_path: str, **kwargs) ‑> None`
:   Download file from dataset
    
    Keyword args:
        organization_name (str): override default organization

    
`list_dataset_volume_files(dataset_name: str, need_download_url: bool = False, path: str = '', recursive: bool = False, **kwargs) ‑> List[openapi_client.models.response_file_metadata.ResponseFileMetadata]`
:   List dataset volume files
    
    Keyword args:
        organization_name (str): override default organization

    
`list_datasets(**kwargs) ‑> List[openapi_client.models.response_dataset_info.ResponseDatasetInfo]`
:   List datasets
    
    Keyword args:
        organization_name (str): override default organization

    
`read_dataset(dataset_name: str, **kwargs) ‑> openapi_client.models.response_dataset_info_detail.ResponseDatasetInfoDetail`
:   Reads a dataset from a default organization and project.
    
    Args:
        `dataset_name` (str): a dataset name
    
    Kwargs:
        organization_name (str): override default organization
    
    Returns:
        A detail information of dataset.
    
    Examples:
    ```python
    dataset = read_dataset(dataset_name="foo")
    ```

    
`read_dataset_version(dataset_id: int, dataset_version_hash: str) ‑> openapi_client.models.response_dataset_version_info.ResponseDatasetVersionInfo`
:   

    
`upload_dataset_volume_file(dataset_name: str, source_path: str, dest_path: str, **kwargs) ‑> None`
:   Upload file to dataset
    
    Keyword args:
        organization_name (str): override default organization