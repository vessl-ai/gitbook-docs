Module vessl.internal.vessl_run
===============================

Classes
-------

`Sender(api: vessl.util.api.VesslApi, experiment_id: int, collectors: List[vessl.internal.collector.Collector])`
:   

    ### Methods

    `start(self)`
    :

    `stop(self)`
    :

`VesslRun()`
:   

    ### Class variables

    `ExitHook`
    :

    ### Instance variables

    `api`
    :   Return an attribute of instance, which is of type owner.

    `hyperparameters`
    :   Return an attribute of instance, which is of type owner.

    ### Methods

    `finish(self)`
    :   Teardown Vessl settings
        
        Use this function to stop tracking your experiment mid-script. If not called,
        tracking is stopped automatically upon exit.
        
        Args:
            path (str): path to upload

    `init(self, experiment_name_or_number=None, message: str = None, tensorboard: bool = False, hp: dict = None, **kwargs)`
    :   Main function to setup Vessl in a local setting
        
        If this is a Vessl-managed experiment or vessl.init has already been called,
        this will do nothing.
        
        Args:
            experiment_name_or_number (str | int): experiment name or number
            message (str): experiment message
            tensorboard (bool): enable tensorboard integration. It is important to note
              that `vessl.init` must be called **before** initializing the writer
              (`tf.summary.create_file_writer` for TF2, SummaryWriter for PyTorch, etc).
            hp (dict): hyperparameters

    `log(self, payload: Dict[str, Any], step: Optional[int] = None, ts: Optional[float] = None)`
    :   Log metrics to Vessl
        
        Args:
            payload (Dict[str, Any]): to log a scalar, value should be a number. To
                log an image, pass a single image or a list of images (type `vessl.util.image.Image`).
            step (int): step.

    `progress(self, value: float)`
    :   Update experiment progress
        
        Args:
            value (float): progress value as a decimal between 0 and 1

    `upload(self, path: str)`
    :   Upload output files
        
        Args:
            path (str): path to upload