Module vessl.util.file_object
=============================

Classes
-------

`UploadableFileObject(url, base_path, path)`
:   

    ### Methods

    `read_in_chunks(filename, chunk_size=65535, chunks=-1, callback=None)`
    :   Lazy function (generator) to read a file piece by piece.

    `upload(self, session=<requests.sessions.Session object>)`
    :

    `upload_chunks(self, *, callback=None)`
    :

    `upload_hooks(self, *, callback=None)`
    :

`UploadableS3Object(local_path: str, bucket, key, token, verbose=False)`
:   

    ### Methods

    `upload(self)`
    :