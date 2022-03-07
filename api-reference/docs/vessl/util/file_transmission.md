Module vessl.util.file_transmission
===================================

Classes
-------

`FileTransmissionHandler(future_func, action: str = 'download', quiet: bool = False)`
:   

    ### Methods

    `add_file(self, full_path, url, size)`
    :

    `run(self)`
    :

`FileTransmissionTracker(total_count, total_size, action)`
:   

    ### Methods

    `increase_done_count(self)`
    :

    `increase_done_size(self, size: int)`
    :

    `print_progress(self, force=False)`
    :

    `print_result(self)`
    :