Module vessl.util.uploader
==========================

Classes
-------

`Uploader()`
:   

    ### Static methods

    `bulk_upload(local_base_path: str, local_file_paths: List[str], volume_id: int, remote_base_path: str) ‑> List[openapi_client.models.response_file_metadata.ResponseFileMetadata]`
    :

    `calculate_crc32c()`
    :

    `get_hashmap(local_base_path)`
    :

    `get_paths_in_dir(local_base_path, hashmap=None)`
    :

    `upload(local_path: str, volume_id: int, remote_path: str) ‑> openapi_client.models.response_file_metadata.ResponseFileMetadata`
    :