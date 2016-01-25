
SaltStack configuration
=======================

OpenStack-Salt Deployment uses Salt configuration platform to install and manage OpenStack. Salt is an automation platform that greatly simplifies system and application deployment. Salt infrastructure uses asynchronous and reliable RAET protocol to communicate and it provides speed of task execution and message transport. 

Salt uses *formulas* to define resources written in the YAML language that orchestrate the individual parts of system into the working entity. For more information, see `Salt Formulas <https://docs.saltstack.com/en/latest/topics/development/conventions/formulas.html>`_.

This guide refers to the host running Salt formulas and metadata service as the *master* and the hosts on which Salt installs the OpenStack-Salt as the *minions*.

A recommended minimal layout for deployments involves five target hosts in total: three infrastructure hosts, and two compute host. All hosts require one network interface. More information on setting up target hosts can be found in `the section called "Server topology" <overview-server-topology.html>`_.

For more information on physical, logical, and virtual network interfaces within hosts see `the section called "Server networking" <overview-server-networking.html>`_.


Using SaltStack
---------------

Remote execution principles carry over all aspects of Salt platform. Command are made of:

- **Target** - Matching minion ID with globbing,  regular expressions, Grains matching, Node groups, compound matching is possible
- **Function** - Commands haveform: module.function, arguments are YAML formatted, compound commands are possible

Try test run to reach minion

.. code-block:: bash

    salt '*' test.version

Targetting minions
~~~~~~~~~~~~~~~~~~

Examples of different kinds of targetting minions

.. code-block:: bash

    salt -E '.*' apache.signal restart
    salt -G 'os:Fedora' test.version
    salt '*' cmd.exec_code python 'import sys; print sys.version'

SaltStack commands
~~~~~~~~~~~~~~~~~~~

Minion facts

.. code-block:: bash

    salt-call grains.items

Minion parameters

.. code-block:: bash

    salt-call pillar.data

Sync state

.. code-block:: bash

    salt-call state.highstate

--------------

.. include:: navigation.txt
