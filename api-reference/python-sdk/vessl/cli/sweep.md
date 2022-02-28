Module vessl.cli.sweep
======================

Functions
---------

    
`parameter_prompter(ctx: click.core.Context, param: click.core.Parameter, value: str) ‑> str`
:   

    
`sweep_name_prompter(ctx: click.core.Context, param: click.core.Parameter, value: str) ‑> str`
:   

Classes
-------

`SweepParameterType()`
:   Represents the type of a parameter. Validates and converts values
    from the command line or Python into the correct type.
    
    To implement a custom type, subclass and implement at least the
    following:
    
    -   The :attr:`name` class attribute must be set.
    -   Calling an instance of the type with ``None`` must return
        ``None``. This is already implemented by default.
    -   :meth:`convert` must convert string values to the correct type.
    -   :meth:`convert` must accept values that are already the correct
        type.
    -   It must be able to convert a value if the ``ctx`` and ``param``
        arguments are ``None``. This can occur when converting prompt
        input.

    ### Ancestors (in MRO)

    * click.types.ParamType

    ### Class variables

    `arity: ClassVar[int]`
    :

    `envvar_list_splitter: ClassVar[Optional[str]]`
    :

    `is_composite: ClassVar[bool]`
    :

    `name: str`
    :

    ### Methods

    `convert(self, raw_value: Any, param, ctx) ‑> Any`
    :   Convert the value to the correct type. This is not called if
        the value is ``None`` (the missing value).
        
        This must accept string values from the command line, as well as
        values that are already the correct type. It may also convert
        other compatible types.
        
        The ``param`` and ``ctx`` arguments may be ``None`` in certain
        situations, such as when converting prompt input.
        
        If the value cannot be converted, call :meth:`fail` with a
        descriptive message.
        
        :param value: The value to convert.
        :param param: The parameter that is using this type to convert
            its value. May be ``None``.
        :param ctx: The current context that arrived at this value. May
            be ``None``.