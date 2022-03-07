Module vessl.integration.tensorboard
====================================

Functions
---------

    
`integrate_tensorboard()`
:   Integrate tensorboard
    
    This method is called from `vessl.init` and can also be called manually.

Classes
-------

`TensorboardCollector()`
:   TensorboardCollector checks for new tensorboard events written to logdir and
    logs them to experiment metrics.
    
    There are two modes: `MODE_TENSORFLOW2` (TF2) and `MODE_OTHERS` (TF1, PyTorch, etc).
    `MODE_OTHERS` uses tensorboard's `EventAccumulator` to read from the event file.
    `MODE_TENSORFLOW2` uses tensorflow's `summary_iterator` because TF2 records events
      in a different way.

    ### Methods

    `close(self)`
    :   Joins thread to stop collecting. Used by tests.

    `set_logdir(self, logdir, mode)`
    :   Called when tensorboard writer is detected. Only the first logdir will be used.

    `start(self)`
    :