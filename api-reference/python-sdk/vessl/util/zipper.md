Module vessl.util.zipper
========================

Classes
-------

`Zipper(file, mode)`
:   Class with methods to open, read, write, close, list zip files.
    
    z = ZipFile(file, mode="r", compression=ZIP_STORED, allowZip64=True,
                compresslevel=None)
    
    file: Either the path to the file, or a file-like object.
          If it is a path, the file will be opened and closed by ZipFile.
    mode: The mode can be either read 'r', write 'w', exclusive create 'x',
          or append 'a'.
    compression: ZIP_STORED (no compression), ZIP_DEFLATED (requires zlib),
                 ZIP_BZIP2 (requires bz2) or ZIP_LZMA (requires lzma).
    allowZip64: if True ZipFile will create files with ZIP64 extensions when
                needed, otherwise it will raise an exception when this would
                be necessary.
    compresslevel: None (default for the given compression type) or an integer
                   specifying the level to pass to the compressor.
                   When using ZIP_STORED or ZIP_LZMA this keyword has no effect.
                   When using ZIP_DEFLATED integers 0 through 9 are accepted.
                   When using ZIP_BZIP2 integers 1 through 9 are accepted.
    
    Open the ZIP file with mode read 'r', write 'w', exclusive create 'x',
    or append 'a'.

    ### Ancestors (in MRO)

    * zipfile.ZipFile

    ### Methods

    `remove(self)`
    :

    `size(self)`
    :

    `zip(self, path)`
    :

    `zipdir(self, path, include_dotfiles=False)`
    :

    `zipfile(self, path)`
    :