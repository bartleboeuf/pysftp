pysftp
======

A simple interface to SFTP.  The module offers high level abstractions and
task based routines to handle your SFTP needs.  Checkout the Cook Book, in the
docs, to see what pysftp can do for you.

Example
-------

::

    import pysftp

    with pysftp.Connection('hostname', username='me', password='secret') as sftp:
        with sftp.cd('public'):             # temporarily chdir to public
            sftp.put('/my/local/filename')  # upload file to public/ on remote
            sftp.get('remote_file')         # get a remote file


::

    import pysftp
    import logging

    logging.basicConfig()
    logging.getLogger("paramiko").setLevel(logging.INFO)

    hostname = "192.168.0.1"
    username = "User1"
    password = "PasswordTest1234!"
    pkPath = "/mnt/c/temp/id_rsa"


    cnopts = pysftp.CnOpts()
    cnopts.log = True            # Activate logging
    cnopts.hostkeys = None       # Ignore KnownHost
    cnopts.server_extensions = {"server-sig-algs": "rsa-sha2-256, ssh-rsa"} # override server extensions
    with pysftp.Connection(
        host=hostname,           # set remote Hostname
        username=username,       # set Username
        password=password,       # set Password
        private_key=pkPath,      # set path to the private key
        private_key_pass=pkPass, # set passphrase of the private key 
        cnopts=cnopts,           # set connection Options
    ) as sftp:
        sftp.put("/tmp/test.tar.gz", "TEMP/test/test2.tar.gz") # Upload file
        print(sftp.listdir())    # List remote directories
        sftp.close()             # Close Connection


Supports
--------
Tested on Python 2.7, 3.2, 3.3, 3.4, 3.8

.. image:: https://drone.io/bitbucket.org/dundeemt/pysftp/status.png
    :target: https://drone.io/bitbucket.org/dundeemt/pysftp/latest
    :alt: Build Status


* Project:  https://bitbucket.org/dundeemt/pysftp
* Download: https://pypi.python.org/pypi/pysftp
* Documentation: http://pysftp.rtfd.org/

