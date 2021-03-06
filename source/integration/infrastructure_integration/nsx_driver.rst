.. _nsx_driver:

NSX Driver
==========

The NSX Driver for OpenNebula enables the interaction with NSX Manager API, to manage its different components, such as logical switches, distributed firewall and so on.

UML diagram
-----------

Here is the dependency between classes into the NSX driver.

.. image:: /images/nsx_driver_classes.png

NSX Integration
---------------

Logical switches integration
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

OpenNebula can manage logical switches using NSX Driver and the hook subsystem. How does it work?

An action to create or delete a logical switch either from Sunstone, CLI or API, generates an specific event.

If there is a hook subscribed to that event, it will execute an action or script.

In the case of NSX, the hook will use the NSX Driver to send commands to the NSX Manager API, and will wait to the answer.

When NSX Manager finish the action, will return a response and the hook, based on that response, will end up as success or error.

The process of creating a logical switch is depicted below.

.. figure:: /images/nsx_driver_integration.png

.. _nsx_object_ref:

Object references
-----------------

All NSX object has its reference within the NSX Manager.

Some NSX objects also has its reference into vCenter Server. This is the case of logical switches, that have its object representation in vCenter.

Here is a table with the components and their reference formats in NSX and vCenter, and also the attributes used in OpenNebula to store that object:

+-----------------------------------+----------+---------------+--------------------------------------+--------------------+
| Object                            | NSX type | ONE Attribute | NSX ref. format                      | vCenter ref format |
+===================================+==========+===============+======================================+====================+
| Logical Switch ( Opaque Network ) | NSX-T    | NSX_ID        | xxxxxxxx-yyyy-zzzz-aaaa-bbbbbbbbbbbb | network-oXXX       |
+-----------------------------------+----------+---------------+--------------------------------------+--------------------+
| Logical Switch ( VirtualWire )    | NSX-V    | NSX_ID        | virtualwire-XXX                      | dvportgroup-XXX    |
+-----------------------------------+----------+---------------+--------------------------------------+--------------------+
| Transport Zone                    | NSX-T    | TZ_ID         | xxxxxxxx-yyyy-zzzz-aaaa-bbbbbbbbbbbb | N/A                |
+-----------------------------------+----------+---------------+--------------------------------------+--------------------+
| Transport Zone                    | NSX-V    | TZ_ID         | vdnscope-XX                          | N/A                |
+-----------------------------------+----------+---------------+--------------------------------------+--------------------+

Managed components
------------------

Currently only Logical Switches are supported. In the image below is shown which components are intended to be supported by OpenNebula through its NSX Driver in the near future.

.. figure:: /images/nsx_driver_managed_components.png
