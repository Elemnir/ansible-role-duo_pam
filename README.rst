======================
 Ansible Role: duo_pam
======================

This ansible role configures a ``duo-auth`` PAM substack to allow integration of one or more Duo TFA applications into authentication systems for services like SSHD.

After running this role, you can add ``auth substack duo-auth`` to any PAM stack to enable Duo.

----------------
 Role Variables
----------------

Key role variables are documented with their default values below. See ``defaults/main.yml`` for a full list.

::

    duo_pam_instances: []

The list of dictionaries defining Duo instances that should appear in the resulting PAM stack in ``/etc/pam.d/duo-auth``. The required keys for each instance are: 

    group
        The Unix group whose users will authenticate against this instance. This role *does not* attempt to create this group.

    filename
        The path where the Duo keys should be stored. This will be owned by, and only readable to root.

    ikey
        The Duo application's integration key. Should not be stored in plaintext.

    skey
        The Duo application's secret key. Should not be stored in plaintext.

    host
        The Duo application's API hostname. 

------------------
 Example Playbook
------------------

::

    ---
    - hosts: localhost
      vars:
        duo_pam_instances:
          - group: duorequired
            filename: /etc/duo/default.conf
            ikey: <duo_ikey>
            skey: <duo_skey>
            host: <duo_host>
      roles:
        - duo_pam
