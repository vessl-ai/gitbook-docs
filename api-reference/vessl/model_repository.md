Module vessl.model_repository
=============================

Functions
---------

    
`create_model_repository(name: str, description: str = None, **kwargs) ‑> openapi_client.models.response_model_repository_detail.ResponseModelRepositoryDetail`
:   Create model repository
    
    Keyword args:
        organization_name (str): override default organization

    
`delete_model_repository(name: str, **kwargs) ‑> object`
:   Delete model repository
    
    Keyword args:
        organization_name (str): override default organization

    
`list_model_repositories(**kwargs) ‑> List[openapi_client.models.response_model_repository_detail.ResponseModelRepositoryDetail]`
:   List model repositories
    
    Keyword args:
        organization_name (str): override default organization

    
`read_model_repository(repository_name: str, **kwargs) ‑> openapi_client.models.response_model_repository_detail.ResponseModelRepositoryDetail`
:   Read model repository
    
    Keyword args:
        organization_name (str): override default organization

    
`update_model_repository(name: str, description: str, **kwargs) ‑> openapi_client.models.response_model_repository_detail.ResponseModelRepositoryDetail`
:   Update model repository
    
    Keyword args:
        organization_name (str): override default organization