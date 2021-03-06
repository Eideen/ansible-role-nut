Ansible Role: NUT
=================
[![Build Status](https://travis-ci.org/ntd/ansible-role-nut.svg?branch=master)](https://travis-ci.org/ntd/ansible-role-nut)

Installs and configures [NUT](http://networkupstools.org/) (Nework UPS
tools) on Debian based systems.

Role Variables
--------------

Available variables are listed below, along with default values (see
`defaults/main.yml`):

    nut_managed_config: true

If this is set to false, none of the following options will have any
effect, that is any and all changes under `/etc/nut/` will be your
responsibility. This is often desirable when you have complex
configurations.

    nut_host: localhost
    nut_user: monitor
    nut_password: Whatever...

Mainly used for configuring the monitor user. A user in the NUT sense is
*not* the typical user a UNIX administrator is used to.

    nut_maxretry: 3

According to the NUT documentation, the default value should mitigate
race with slow devices.

    nut_ups:
      - name: UPS
        driver: riello_ups
        device: /dev/ttyUSB0
        description: Some descriptive information

`name` and `description` are arbitrary values used for debugging and
reporting purposes.

`driver` depends on your hardware and must be one of the [available NUT
driver](http://networkupstools.org/stable-hcl.html). Be sure the NUT
version installed on your server has that specific driver available.

`device` is device where the UPS is listening (typically an USB port or
a serial device).

Example Playbook
----------------

    - hosts: all
      roles:
      - role: ntd.nut
        nut_ups:
          - name: riello
            driver: riello_usb
            device: /dev/ups
            description: iPlug 800

License
-------

MIT

Author Information
------------------

This role was created in 2016 by Nicola Fontana (ntd@entidi.it).
