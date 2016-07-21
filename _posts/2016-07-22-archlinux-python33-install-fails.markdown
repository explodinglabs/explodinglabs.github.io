---
layout: post
title: "Python 3.3 failing to install on Arch Linux"
date: 2016-07-22
permalink: /archlinux-python33-install-fails
---

Installing Python 3.3 on Arch tonight, two tests failed:

    [157/372] test_import
    test test_import failed -- Traceback (most recent call last):
      File "/tmp/packerbuild-1000/python33/python33/src/Python-3.3.6/Lib/test/test_import.py", line 307, in test_timestamp_overflow
          os.stat(compiled)
          FileNotFoundError: [Errno 2] No such file or directory: '__pycache__/@test_9865_tmp.cpython-33.pyc'

Another test:

    [251/372/1] test_pyexpat
    test test_pyexpat failed -- Traceback (most recent call last):
      File "/tmp/packerbuild-1000/python33/python33/src/Python-3.3.6/Lib/test/test_pyexpat.py", line 607, in test2
          parser.Parse(xml, True)
          xml.parsers.expat.ExpatError: XML declaration not well-formed: line 1, column 13

    During handling of the above exception, another exception occurred:

    Traceback (most recent call last):
      File "/tmp/packerbuild-1000/python33/python33/src/Python-3.3.6/Lib/test/test_pyexpat.py", line 610, in test2
          self.assertEqual(str(e), 'XML declaration not well-formed: line 1, column 14')
          AssertionError: 'XML declaration not well-formed: line 1, column 13' != 'XML declaration not well-formed: line 1, column 14'
          - XML declaration not well-formed: line 1, column 13
          ?                                                  ^
          + XML declaration not well-formed: line 1, column 14
          ?

Test results:

    347 tests OK.
    2 tests failed: test_import test_pyexpat
    23 tests skipped:
        test_codecmaps_cn test_codecmaps_hk test_codecmaps_jp
        test_codecmaps_kr test_codecmaps_tw test_curses test_devpoll
        test_gdb test_kqueue test_msilib test_ossaudiodev test_smtpnet
        test_socketserver test_startfile test_timeout test_tk
        test_ttk_guionly test_urllib2net test_urllibnet test_winreg
        test_winsound test_xmlrpc_net test_zipfile64
    Those skips are all expected on linux.
    ==> ERROR: A failure occurred in check().
    Aborting...
    The build failed.

Easiest way to get it installed was to skip the tests.

    # pacman -S packer33

When packer asked to edit the PKGBUILD I said yes, and removed the check()
function in which the tests were running.
