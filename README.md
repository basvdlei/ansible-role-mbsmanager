mbs-manager
===========

This role will build and run mbs-manager for Minecraft Bedrock Server from
Mojang on your target host.

mbs-manager wraps around the stdin/stdout from the server so it can be managed
using a local HTTP server.

**NOTE**: mbs-manager is NOT OFFICIAL MINECRAFT PRODUCT. NOT APPROVED BY OR
ASSOCIATED WITH MOJANG.

Requirements
------------

This role will download the given version of Server Software for Minecraft as
found on: https://www.minecraft.net/en-us/download/server/bedrock You will need
to agree with the legal documents (EULA and Privacy Policy) and change the
`mbs_manager_upstream_license` role variable to "accept" to use this role.

A `server.properties` must be provided by placing it in the playbook's `files`.
An example can be found inside the server software download from
https://www.minecraft.net/en-us/download/server/bedrock

Role Variables
--------------

Available variables are listed below, along with default values (see
`defaults/main.yml`):

	mbs_manager_upstream_license: "notaccepted"

Indication if the role consumer has read and agreed to the legal documents
required to download and use the Server Software for Minecraft. Value should be
`accept` or the role will exit.

	mbs_manager_version: "1.16.221.01"

Server Software for Minecraft version to download, build and run.

	mbs_manager_datadir: /srv/minecraft-bedrock-data

Target directory for the server and world data.

	mbs_manager_permissions_file: default-permissions.json

Filename for the initial `permissions.json` to install. Afterwards the server
software will take over managing the contents of this file. A default empty
permissions file is included in this role.

	mbs_manager_properties_file: server.properties

Filename of the `server.properties` to install from the Ansible src files.
**Note:** a server.properties file needs to be provided.

	mbs_manager_whitelist_file: default-whitelist.json

Filename for the initial `permissions.json` to install. Afterwards the server
software will take over managing the contents of this file. A default empty
whitelist file is included in this role.

	mbs_manager_initial_state_name

Optional name of the world of the initial state that needs to be restored. This
name needs to match the name of the world as defined in the given
`server.properties`.

	mbs_manager_initial_state_archive

Optional filename of an archive of world data to restore as the initial world.
It needs to include the world directory eg. `myworld/level.dat` that matches
the given `mbs_manager_initial_state_name` and world name in
`server.properties`.

Dependencies
------------

- Docker: https://github.com/basvdlei/ansible-role-docker

Example Playbook
----------------

    - hosts: servers
      roles:
         - { role: mbs-manager, mbs_manager_upstream_license: "notaccepted" }

License
-------

BSD 3-Clause
