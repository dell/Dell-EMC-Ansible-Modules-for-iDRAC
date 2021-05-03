# Dell EMC OpenManage Ansible Modules

Dell EMC OpenManage Ansible Modules allows data center and IT administrators to use RedHat Ansible to automate and orchestrate the configuration, deployment, and update of Dell EMC PowerEdge Servers and modular infrastructure by leveraging the management automation capabilities in-built into the Integrated Dell Remote Access Controller (iDRAC), OpenManage Enterprise and OpenManage Enterprise Modular.

OpenManage Ansible Modules simplifies and automates provisioning, deployment, and updates of PowerEdge servers and modular infrastructure. It allows system administrators and software developers to introduce the physical infrastructure provisioning into their software provisioning stack, integrate with existing DevOps pipelines and manage their infrastructure using version-controlled playbooks, server configuration profiles, and templates in line with the Infrastructure-as-Code (IaC) principles.

- [Supported Platforms](#supported-platforms)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Sample Playbooks](#sample-playbooks)
- [Handling Modules with Required Shares](#handling-modules-with-required-shares)
  - [Why is a share required?](#why-is-a-share-required)
  - [How to handle required shares easily](#how-to-handle-required-shares-easily)
- [Documentation](#documentation)
- [LICENSE](#license)
- [Contributing](#contributing)
- [Testing](#testing)
- [Maintenance](#maintenance)
- [Support](#support)
- [Authors](#authors)

## Supported Platforms
  * iDRAC 7 and 8 based Dell EMC PowerEdge Servers with Firmware versions 2.60.60.60 and above.
  * iDRAC 9 based Dell EMC PowerEdge Servers with Firmware versions 3.34.34.34 and above.
  * Dell EMC OpenManage Enterprise versions 3.2.1 and above.
  * Dell EMC OpenManage Enterprise-Modular versions 1.20.00 and above.

## Prerequisites
  * [Ansible >= 2.10.0](https://github.com/ansible/ansible)
  * Python >=2.7.17 or >=3.6.5
  * To run the iDRAC modules, install OpenManage Python Software Development
   Kit (OMSDK) using ``` pip install omsdk --upgrade``` or from 
   [Dell EMC OpenManage Python SDK](https://github.com/dell/omsdk)

## Installation

* From [galaxy](https://galaxy.ansible.com/dellemc/openmanage):  
```ansible-galaxy collection install dellemc.openmanage```

    - For offline installation on the Ansible control machine, download the required tar archive version of the collection from [Dell EMC OpenManage collection](https://galaxy.ansible.com/dellemc/openmanage) and run the command given below:  
      ```ansible-galaxy collection install dellemc-openmanage-<version>.tar.gz```

* From [github](https://github.com/dell/dellemc-openmanage-ansible-modules/tree/collections):  
Install the collection from the github repository using the latest commit on the branch 'collections'  
```ansible-galaxy collection install git+https://github.com/dell/dellemc-openmanage-ansible-modules.git,collections```

## Sample Playbooks
Latest sample playbooks and examples are available at [playbooks](https://github.com/dell/dellemc-openmanage-ansible-modules/tree/collections/playbooks).

## Handling Modules with Required Shares

### Why is a share required?

Many modules use what's called a server configuration profile (SCP) to update the iDRAC attributes on iDRAC 7/8 and iDRAC 9.
When we were first developing these Ansible modules, iDRAC7/8 only supported importing a SCP file from a remote 
network share (CIFS or NFS). Subsquently share_name argument was added to specify the network share location that
iDRAC uses to import the SCP. iDRAC7/8 now also support local file streaming within the HTTPS message playload itself
(firmare version 2.50.50.50 and above). We are currently working to update the modules to leverage these new mechanisms.
For a detailed explanation see [this post](https://github.com/dell/omsdk/blob/devel/docs/idrac.rst#prerequisites)

### How to handle required shares easily

In the meantime, you do not actually need to provide a share. You can pass {{ playbook_dir }} to share name like this:

      - name: Setup iDRAC NIC
        idrac_network:
           idrac_ip:   "{{ idrac_ip }}"
           idrac_user: "{{ idrac_user }}"
           idrac_password:  "{{ idrac_password }}"
           share_name: "{{ playbook_dir }}"
           enable_nic: "Enabled"
           nic_selection: "Dedicated"
           failover_network: "T_None"
           auto_detect: "Disabled"
           auto_negotiation: "Enabled"
           network_speed: "T_1000"
           duplex_mode: "Full"
    
        tags:
           - idrac_nic

or if you are debugging a module it would look like this:

    {
        "ANSIBLE_MODULE_ARGS": {
            "idrac_ip": "192.168.1.63",
            "idrac_user": "root",
            "idrac_password": "calvin",
            "share_name": "/home/gelante/programs/dellemc-openmanage-ansible-modules",
            "ip_address": "192.168.1.64"
        }
    }

## Documentation
Use `ansible-doc` to view the documentation of each module and plugin.  
For example-```ansible-doc dellemc.openmanage.<module_name>```  

## LICENSE
This project is licensed under GPL-3.0 License. See the [COPYING](https://github.com/dell/dellemc-openmanage-ansible-modules/tree/collections/COPYING.md) for more information.

## Contributing
We welcome your contributions to OpenManage Ansible Modules. See [Coding Guidelines](https://github.com/dell/dellemc-openmanage-ansible-modules/tree/collections/CODING_GUIDELINES.md) for more details.
You can refer our [Code of Conduct](https://github.com/dell/dellemc-openmanage-ansible-modules/tree/collections/CODE_OF_CONDUCT.md) here.

## Testing
See [here](https://github.com/dell/dellemc-openmanage-ansible-modules/tree/collections/tests/README.md) for further information on testing.

## Maintenance
  * OpenManage Ansible Modules releases follows a monthly release cycle. On the last week of every month, 
  the updated modules are posted to this repository.
  * OpenManage Ansible Modules releases follow [semantic versioning](https://semver.org/).
  * OpenManage Ansible Modules deprecation cycle is aligned with [Ansible](https://docs.ansible.com/ansible/latest/dev_guide/module_lifecycle.html).

## Support
  * This branch corresponds to the release actively under development.
  * To report any issue, create an issue [here](https://github.com/dell/dellemc-openmanage-ansible-modules/issues).
  * If any requirements have not been addressed, then create an issue [here](https://github.com/dell/dellemc-openmanage-ansible-modules/issues).
  * To provide feedback to the development team, send an email to **OpenManageAnsible@Dell.com**.

## Authors
  * OpenManageAnsible (OpenManageAnsible@dell.com)
