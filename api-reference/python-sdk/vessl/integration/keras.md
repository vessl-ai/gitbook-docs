Module vessl.integration.keras
==============================

Classes
-------

`ExperimentCallback(data_type=None, validation_data=None, num_images=None, labels=None, start_epoch=0, save_image=False)`
:   Abstract base class used to build new callbacks.
    
    Callbacks can be passed to keras methods such as `fit`, `evaluate`, and
    `predict` in order to hook into the various stages of the model training and
    inference lifecycle.
    
    To create a custom callback, subclass `keras.callbacks.Callback` and override
    the method associated with the stage of interest. See
    https://www.tensorflow.org/guide/keras/custom_callback for more information.
    
    Example:
    
    >>> training_finished = False
    >>> class MyCallback(tf.keras.callbacks.Callback):
    ...   def on_train_end(self, logs=None):
    ...     global training_finished
    ...     training_finished = True
    >>> model = tf.keras.Sequential([tf.keras.layers.Dense(1, input_shape=(1,))])
    >>> model.compile(loss='mean_squared_error')
    >>> model.fit(tf.constant([[1.0]]), tf.constant([[1.0]]),
    ...           callbacks=[MyCallback()])
    >>> assert training_finished == True
    
    If you want to use `Callback` objects in a custom training loop:
    
    1. You should pack all your callbacks into a single `callbacks.CallbackList`
       so they can all be called together.
    2. You will need to manually call all the `on_*` methods at the appropriate
       locations in your loop. Like this:
    
       ```
       callbacks =  tf.keras.callbacks.CallbackList([...])
       callbacks.append(...)
    
       callbacks.on_train_begin(...)
       for epoch in range(EPOCHS):
         callbacks.on_epoch_begin(epoch)
         for i, data in dataset.enumerate():
           callbacks.on_train_batch_begin(i)
           batch_logs = model.train_step(data)
           callbacks.on_train_batch_end(i, batch_logs)
         epoch_logs = ...
         callbacks.on_epoch_end(epoch, epoch_logs)
       final_logs=...
       callbacks.on_train_end(final_logs)
       ```
    
    Attributes:
        params: Dict. Training parameters
            (eg. verbosity, batch size, number of epochs...).
        model: Instance of `keras.models.Model`.
            Reference of the model being trained.
    
    The `logs` dictionary that callback methods
    take as argument will contain keys for quantities relevant to
    the current batch or epoch (see method-specific docstrings).

    ### Ancestors (in MRO)

    * keras.callbacks.Callback

    ### Methods

    `on_epoch_end(self, epoch, logs=None)`
    :   Called at the end of an epoch.
        
        Subclasses should override for any actions to run. This function should only
        be called during TRAIN mode.
        
        Args:
            epoch: Integer, index of epoch.
            logs: Dict, metric results for this training epoch, and for the
              validation epoch if validation is performed. Validation result keys
              are prefixed with `val_`. For training epoch, the values of the
             `Model`'s metrics are returned. Example : `{'loss': 0.2, 'accuracy':
               0.7}`.

`ModelCallback(upload_policy: str = 'always', objective: str = None, target_metric: str = None, description: str = None, tags: List[str] = [])`
:   Abstract base class used to build new callbacks.
    
    Callbacks can be passed to keras methods such as `fit`, `evaluate`, and
    `predict` in order to hook into the various stages of the model training and
    inference lifecycle.
    
    To create a custom callback, subclass `keras.callbacks.Callback` and override
    the method associated with the stage of interest. See
    https://www.tensorflow.org/guide/keras/custom_callback for more information.
    
    Example:
    
    >>> training_finished = False
    >>> class MyCallback(tf.keras.callbacks.Callback):
    ...   def on_train_end(self, logs=None):
    ...     global training_finished
    ...     training_finished = True
    >>> model = tf.keras.Sequential([tf.keras.layers.Dense(1, input_shape=(1,))])
    >>> model.compile(loss='mean_squared_error')
    >>> model.fit(tf.constant([[1.0]]), tf.constant([[1.0]]),
    ...           callbacks=[MyCallback()])
    >>> assert training_finished == True
    
    If you want to use `Callback` objects in a custom training loop:
    
    1. You should pack all your callbacks into a single `callbacks.CallbackList`
       so they can all be called together.
    2. You will need to manually call all the `on_*` methods at the appropriate
       locations in your loop. Like this:
    
       ```
       callbacks =  tf.keras.callbacks.CallbackList([...])
       callbacks.append(...)
    
       callbacks.on_train_begin(...)
       for epoch in range(EPOCHS):
         callbacks.on_epoch_begin(epoch)
         for i, data in dataset.enumerate():
           callbacks.on_train_batch_begin(i)
           batch_logs = model.train_step(data)
           callbacks.on_train_batch_end(i, batch_logs)
         epoch_logs = ...
         callbacks.on_epoch_end(epoch, epoch_logs)
       final_logs=...
       callbacks.on_train_end(final_logs)
       ```
    
    Attributes:
        params: Dict. Training parameters
            (eg. verbosity, batch size, number of epochs...).
        model: Instance of `keras.models.Model`.
            Reference of the model being trained.
    
    The `logs` dictionary that callback methods
    take as argument will contain keys for quantities relevant to
    the current batch or epoch (see method-specific docstrings).

    ### Ancestors (in MRO)

    * keras.callbacks.Callback

    ### Methods

    `on_train_end(self, logs=None)`
    :   Called at the end of training.
        
        Subclasses should override for any actions to run.
        
        Args:
            logs: Dict. Currently the output of the last call to `on_epoch_end()`
              is passed to this argument for this method but that may change in
              the future.