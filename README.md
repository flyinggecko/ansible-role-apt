apt
===

Role for managing your apt sources and preferences.

Requirements
------------

None

Role Variables
--------------

`apt_pin_dir`: Directory where the apt pins are kept (/etc/apt/preferences.d/pattern)

`apt_source_state`: Temporary variable to get the state of the apt source

`apt_source_{host,group,all}`: An array with sources for apt

    apt_source_{host,group,all}:
      - source: {deb,deb-src} source-url Distribution Component
        state: {present,absent} (optional, defaults to present)
        key:
          id: key-id (optional)
          keyserver: keyserver-url (optinal)
          url: url to a public-key-file (optional)
          gpg_file: gpg-file in files-dir (optional)
*when one of keyserver,url or gpg_file is used, the id should be used for retrieving and verifying*

`apt_pin_{host,group,all}`: An array with pins for apt

    apt_pin_{host,group,all}:
      - pattern: ^Iceweasel (required)
        pin: release a=testing (required)
        priority: 600 (optional, defaults to 200)
        filepath: /etc/apt/preferences.d/iceweacel (optional, defaults to apt_pin_dir)
        state: {present,absent} (optional, defaults to present)


Dependencies
------------

None

Example Playbook
----------------

`some_vars_file.yml`:

    apt_source_all:
      - source: "deb http://http.debian.net/debian stable main"
        state: "present"
        key:
          id: "65FFB764"
          keyserver: keys.gnupg.net

    apt_pin_all:
      - pattern: "*"
        pin: "release a=stable"
        priority: "900"
        filepath: "/etc/apt/preferences.d/stable"

`some_playbook.yml`:

    - hosts: webserver
      sudo: yes
      roles:
      - apt

License
-------

The MIT License (MIT)

Copyright (c) 2014 Julian Stiller

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

Author Information
------------------

This role was inspired by ajsalminen.apt_source, but totally rewritten

Contributing
------------

I welcome contributed improvements and bug fixes via the usual github
workflow:

1. Fork this repository
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new pull request
