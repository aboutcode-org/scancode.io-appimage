ScanCode.io AppImage
--------------------

This repo provides `scancode.io <https://github.com/nexb/scancode.io>`_ as an AppImage. Specifically, AppImage is built using `pkg2appimage <https://github.com/AppImageCommunity/pkg2appimage>`_, which packages scancode.io from https://github.com/nexb/scancode.io/tree/scancode.io-appimage, Python built from `Python-Linux-Support <https://github.com/beeware/Python-Linux-support>`_, and other ScanCode Toolkit system dependencies into an AppImage.

Usage
-----

Note: scancode.io will be run using the Django development server. The entry point of the scancode.io AppImage points to ``manage.py`` of scancode.io.

Ensure that the AppImage is executable:
    - ``chmod +x scancodeio-.glibc2.27-x86_64.AppImage``

To use the scancode.io AppImage, you will need to have some environmental variables set:
    - ``SCANCODEIO_DB_NAME``
        - This contains the absolute path to the sqlite file that will be used to store scancode.io's database.

    - ``SCANCODEIO_WORKSPACE_LOCATION``
        - This contains the absolute path to a directory where scancode.io can store project files.

Before running the server, you will need to create the sqlite file used for scancode.io's database:
    - ``SCANCODEIO_DB_NAME="<path to scancodeio.db>" SCANCODEIO_WORKSPACE_LOCATION="<path to scancodeio workspace directory>" scancodeio-.glibc2.27-x86_64.AppImage migrate``

To run the server:
    - ``SCANCODEIO_DB_NAME="<path to scancodeio.db>" SCANCODEIO_WORKSPACE_LOCATION="<path to scancodeio workspace directory>" scancodeio-.glibc2.27-x86_64.AppImage runserver --insecure``

scancode.io will now be available at http://127.0.0.1:8000
