Module vessl.model
==================

Functions
---------

    
`create_model(repository_name: str, repository_description: str = None, experiment_id: int = None, model_name: str = None, paths: List[str] = None, **kwargs) ‑> openapi_client.models.response_model_detail.ResponseModelDetail`
:   Create model
    
    Keyword args:
        organization_name (str): override default organization

    
`delete_model(repository_name: str, number: int, **kwargs) ‑> object`
:   Delete model
    
    Keyword args:
        organization_name (str): override default organization

    
`delete_model_volume_file(repository_name: str, model_number: int, path: str, recursive: bool = False, **kwargs) ‑> List[openapi_client.models.response_file_metadata.ResponseFileMetadata]`
:   Delete model volume file
    
    Keyword args:
        organization_name (str): override default organization

    
`download_model_volume_file(repository_name: str, model_number: int, source_path: str, dest_path: str, **kwargs) ‑> None`
:   Download file to model
    
    Keyword args:
        organization_name (str): override default organization

    
`list_model_volume_files(repository_name: str, model_number: int, need_download_url: bool = False, path: str = '', recursive: bool = False, **kwargs) ‑> List[openapi_client.models.response_file_metadata.ResponseFileMetadata]`
:   List model files
    
    Keyword args:
        organization_name (str): override default organization

    
`list_models(repository_name: str, **kwargs) ‑> List[openapi_client.models.response_model_detail.ResponseModelDetail]`
:   List models
    
    Keyword args:
        organization_name (str): override default organization

    
`read_model(repository_name: str, model_number: int, **kwargs) ‑> openapi_client.models.response_model_detail.ResponseModelDetail`
:   Read model
    
    Keyword args:
        organization_name (str): override default organization

    
`update_model(repository_name: str, number: int, name: str, **kwargs) ‑> openapi_client.models.response_model_detail.ResponseModelDetail`
:   Update model
    
    Keyword args:
        organization_name (str): override default organization

    
`upload_model_volume_file(repository_name: str, model_number: int, source_path: str, dest_path: str, **kwargs) ‑> None`
:   Upload file to model
    
    Keyword args:
        organization_name (str): override default organization