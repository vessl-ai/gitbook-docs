Module vessl.volume
===================

Functions
---------

    
`copy_volume_file(source_volume_id: Optional[int], source_path: str, dest_volume_id: Optional[int], dest_path: str, recursive: bool = False, quiet: bool = False) ‑> Optional[List[openapi_client.models.response_file_metadata.ResponseFileMetadata]]`
:   

    
`create_volume_file(volume_id: int, is_dir: bool, path: str) ‑> openapi_client.models.response_file_metadata.ResponseFileMetadata`
:   

    
`delete_volume_file(volume_id: int, path: str, recursive: bool = False) ‑> List[openapi_client.models.response_file_metadata.ResponseFileMetadata]`
:   

    
`list_volume_files(volume_id: int, need_download_url: bool = False, path: str = '', recursive: bool = False) ‑> List[openapi_client.models.response_file_metadata.ResponseFileMetadata]`
:   

    
`read_volume_file(volume_id: int, path: str) ‑> openapi_client.models.response_file_metadata.ResponseFileMetadata`
:   

    
`upload_volume_file(volume_id: int, path: str) ‑> openapi_client.models.response_file_metadata.ResponseFileMetadata`
: