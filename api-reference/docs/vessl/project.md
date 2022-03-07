Module vessl.project
====================

Functions
---------

    
`create_project(project_name: str, description: str = None, **kwargs) ‑> openapi_client.models.response_project_info.ResponseProjectInfo`
:   Create project
    
    Keyword args:
        organization_name (str): override default organization

    
`list_projects(**kwargs) ‑> List[openapi_client.models.response_project_info.ResponseProjectInfo]`
:   List projects
    
    Keyword args:
        organization_name (str): override default organization

    
`read_project(project_name: str, **kwargs) ‑> openapi_client.models.response_project_info.ResponseProjectInfo`
:   Read project
    
    Keyword args:
        organization_name (str): override default organization