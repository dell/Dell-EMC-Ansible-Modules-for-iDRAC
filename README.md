# Dell EMC OpenManage Ansible Modules

Dell EMC OpenManage Ansible Modules allows Data Center and IT administrators to use RedHat Ansible to automate and orchestrate the configuration, deployment, and update of Dell EMC PowerEdge Servers (12th generation of PowerEdge servers and later) by leveraging the management automation capabilities in-built into the integrated Dell Remote Access Controller (iDRAC).

With the latest release of Dell EMC OpenManage Ansible Modules, the capabilities have improved with support for OpenManage Enterprise. OpenManage Ansible Modules allows users to retrieve device inventory information of each device discovered in the OpenManage Enterprise.

## Supported Platforms
Dell EMC PowerEdge Servers with:
  * 12G and 13G PowerEdge Servers: iDRAC 7/8 with Firmware version 2.60.60.60 and above
  * 14G PowerEdge Servers: iDRAC 9 with Firmware version 3.21.21.21 and above

## Prerequisites
  * [Ansible](https://github.com/ansible/ansible)
  * Python >= 2.7.5
  * For OpenManage Ansible modules for iDRAC, install the supported version of [Dell EMC OpenManage Python SDK](https://github.com/dell/omsdk)

## Documentation
Please refer to the [OpenManage Ansible Modules Documentation](./guides)

## Examples
Sample playbooks and examples could be found under [examples](./examples) directory

## Results
Sample Results for the respective modules could be found under [samples](./samples) directory.

## Installation

  * Clone the latest development repository and install the ansible modules. 
  ```
  git clone -b devel --single-branch https://github.com/dell/dellemc-openmanage-ansible-modules.git
  cd dellemc-openmanage-ansible-modules
  python install.py
  ```

  * It is recommended to update the ansible configuration setting environment variables to point to the current module paths, if any.

## Uninstallation

```
cd dellemc-openmanage-ansible-modules
python uninstall.py
```

## Docker image for OpenManage Ansible Modules
The containerized version of the OpenManage Ansible Modules is available in the [Docker Store](https://hub.docker.com/r/dellemc/openmanage-ansible-modules). Refer following [how-to guide](./docker/README.md) with instructions on how to use the container.

## LICENSE
This project is licensed under GPL-3.0 License. Please see the [COPYING](
https://github.com/dell/dellemc-openmanage-ansible-modules/blob/master/COPYING.md) for more information

## Support
  * This devel branch corresponds to the release actively under development.
  * If you want to report any issue, then please report it by creating a new issue [here](https://github.com/dell/dellemc-openmanage-ansible-modules/issues)
  * If you have any requirements that is not currently addressed, then please let us know by creating a new issue [here](https://github.com/dell/dellemc-openmanage-ansible-modules/issues)
  * If you want to provide any feedback to the development team, then you can do so by sending an email to **OpenManageAnsible@Dell.com**
  * We also have a **#openmanageansible** slack channel which you can use for reporting any issue, new feature request or for general discussion with development team. You can get an invite by requesting one at [here](http://community.codedellemc.com).

## Authors
  * OpenManageAnsible (OpenManageAnsible@dell.com)
