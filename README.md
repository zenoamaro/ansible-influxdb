InfluxDB for Ansible
======================
A role for deploying and configuring [InfluxDB](http://influxdb.com) on unix hosts using [Ansible](http://www.ansibleworks.com).

It can additionally be used as a playbook for quickly provisioning hosts.

Vagrant machines are provided to produce a boxed install of InfluxDB or a VM for integration testing.


Supports
--------
Supported InfluxDB versions:
- InfluxDB ^0.8

Supported targets:
- Ubuntu 14.04 LTS "Trusty Tahr"
- Ubuntu 12.04 LTS "Precise Pangolin"
- Debian (untested)
- RedHat (untested)

Installation methods:
- Official packages from [InfluxDB](http://influxdb.com/docs/v0.8/introduction/installation.html)


Usage
-----
Clone this repo into your roles directory:

    $ git clone https://github.com/zenoamaro/ansible-influxdb.git roles/influxdb

And add it to your play's roles:

    - hosts: ...
      roles:
        - influxdb
        - ...

This roles comes preloaded with almost every available default. You can override each one in your hosts/group vars, in your inventory, or in your play. See the annotated defaults in [defaults/main.yml](defaults/main.yml) for help in configuration. All provided variables start with `influxdb_`.

You may want to pin your influxdb version by setting `influxdb_version`, otherwise `latest` will be installed.

You can also use the role as a playbook. You will be asked which hosts to provision, and you can further configure the play by using `--extra-vars`.

    $ ansible-playbook -i inventory --extra-vars='{...}' main.yml

To provision a standalone box, start the `boxed` VM, which is a Ubuntu 14.04 box. After that, you can login to the admin interface on the host (on `18083` by default) as user `root` and password `root`. You will similarly find the API available (on `18086` by default) with the same credentials.

    $ vagrant up boxed

Run the tests by provisioning the appropriate VM:

    $ vagrant up test-ubuntu-trusty

At the moment, the following test boxes are available:

- `test-ubuntu-precise`
- `test-ubuntu-trusty`


Still to do
-----------
- Test on RedHat
- Syslog
- Unlimited files
- Better configuration for input storages and dbs using hashes?


Changelog
---------
### next
- Script directory is now being created during configuration. Fixes #1.
- Fixed double slashes when producing instance paths. Fixes #1.

### 0.1.1
- The package list is not being updated in playbooks anymore.
- VMs are not autostarted anymore.
- Updated inventory to use the new Vagrant private keys.

### 0.1.0
Initial version.


License
-------
The MIT License (MIT)

Copyright (c) 2015, zenoamaro <zenoamaro@gmail.com>

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.