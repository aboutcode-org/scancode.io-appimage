ScanCode.io AppImage
--------------------

This repo provides `scancode.io <https://github.com/nexb/scancode.io>`_ as an
AppImage. Specifically, AppImage is built using the build files found at
https://github.com/nexB/scancode.io/tree/scancode.io-appimage/etc/scripts/appimage-build,
which uses `pkg2appimage <https://github.com/AppImageCommunity/pkg2appimage>`_
to package scancode.io, Python built from `python-appimage
<https://github.com/niess/python-appimage>`_, and other ScanCode Toolkit
system dependencies into an AppImage.

Usage
-----

Note: scancode.io will be run using the Django development server. The entry
point of the scancode.io AppImage points to ``manage.py`` of scancode.io.

Ensure that the AppImage is executable:
    - ``chmod +x scancodeio-*glibc2.27-x86_64.AppImage``

On first run, the file ``.env-scancodeio`` will be created in your home
directory with environment variables necessary to run scancode.io from an
AppImage:
    - ``SECRET_KEY``
        - Used for generating cryptographic hashes. This key is randomly
          generated and must be kept secret.
    - ``SCANCODEIO_DB_ENGINE``
        - This determines the database backend used by scancode.io.
        - By default, this is set to ``django.db.backends.sqlite3``, as the
          scancode.io AppImage only supports using a sqlite database.
    - ``SCANCODEIO_DB_NAME``
        - This contains the absolute path to the sqlite file that will be used
          to store scancode.io's database.
        - By default, a file named ``scancodeio.db`` will be created in the
          user's home directory.
    - ``SCANCODEIO_WORKSPACE_LOCATION``
        - This contains the absolute path to a directory where scancode.io can
          store project files.
        - By default, a directory named ``scancodeio-workspace`` will be created
          the user's home directory.

Other environment variables can be set in the ``.env-scancodeio`` file. You can
see what environment variables can be set from the variables in
https://github.com/nexB/scancode.io/blob/scancode.io-appimage/scancodeio/settings.py

For example, if you wanted to adjust the time taken to scan a file in
scancode.io, you can set the duration using the ``SCANCODEIO_SCAN_FILE_TIMEOUT``
environment variable.

In the case of where you will be deploying scancode.io to a server, you must add
that server's hostname to the ``ALLOWED_HOSTS`` environment variable before you
are able to access it externally.

Before running the server, you will need to create the sqlite file used for
scancode.io's database and run database migrations:
    - ``./scancodeio-*glibc2.27-x86_64.AppImage migrate``

To run the server:
    - ``./scancodeio-*glibc2.27-x86_64.AppImage runserver --insecure``

scancode.io will now be available at http://127.0.0.1:8000
