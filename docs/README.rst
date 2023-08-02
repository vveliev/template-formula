.. _readme:

TEMPLATE-formula
================

|img_travis| |img_sr| |img_pc|

.. |img_travis| image:: https://travis-ci.com/saltstack-formulas/TEMPLATE-formula.svg?branch=master
   :alt: Travis CI Build Status
   :scale: 100%
   :target: https://travis-ci.com/saltstack-formulas/TEMPLATE-formula
.. |img_sr| image:: https://img.shields.io/badge/%20%20%F0%9F%93%A6%F0%9F%9A%80-semantic--release-e10079.svg
   :alt: Semantic Release
   :scale: 100%
   :target: https://github.com/semantic-release/semantic-release
.. |img_pc| image:: https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit&logoColor=white
   :alt: pre-commit
   :scale: 100%
   :target: https://github.com/pre-commit/pre-commit

A SaltStack formula that is empty. It has dummy content to help with a quick
start on a new formula and it serves as a style guide.

.. contents:: **Table of Contents**
   :depth: 1

Getting started
---------------

.. <REMOVEME

Using this template
^^^^^^^^^^^^^^^^^^^

The easiest way to use this template formula as a base for a new formula is to use GitHub's **Use this template** button to create a new repository. For consistency with the rest of the formula ecosystem, name your formula repository following the pattern ``<formula theme>-formula``, where ``<formula theme>`` consists of lower-case alphabetic characters, numbers, '-' or '_'.

In the rest of this example we'll use ``example`` as the ``<formula theme>``.

Follow these steps to complete the conversion from ``template-formula`` to ``example-formula``. ::

  $ git clone https://github.com/saltstack-formulas/template-formula example-formula
  $ cd example-formula/
  $ bin/convert-formula.sh example

.. REMOVEME>

Available states
^^^^^^^^^^^^^^^^
.. contents::
   :local:

``TEMPLATE``
~~~~~~~~~~~~

*Meta-state (This is a state that includes other states)*.

This installs the TEMPLATE package,
manages the TEMPLATE configuration file and then
starts the associated TEMPLATE service.

``TEMPLATE.package``
~~~~~~~~~~~~~~~~~~~~
This state will install the TEMPLATE package only.

``TEMPLATE.config``
~~~~~~~~~~~~~~~~~~~~

This state will configure the TEMPLATE service and has a dependency on ``TEMPLATE.install``
via include list.

``TEMPLATE.service``
~~~~~~~~~~~~~~~~~~~~
This state will start the TEMPLATE service and has a dependency on ``TEMPLATE.config``
via include list.

``TEMPLATE.clean``
~~~~~~~~~~~~~~~~~~

*Meta-state (This is a state that includes other states)*.

this state will undo everything performed in the ``TEMPLATE`` meta-state in reverse order, i.e.
stops the service,
removes the configuration file and
then uninstalls the package.

``TEMPLATE.service.clean``
~~~~~~~~~~~~~~~~~~~~~~~~~~

This state will stop the TEMPLATE service and disable it at boot time.

``TEMPLATE.config.clean``
~~~~~~~~~~~~~~~~~~~~~~~~~

This state will remove the configuration of the TEMPLATE service and has a
dependency on ``TEMPLATE.service.clean`` via include list.

``TEMPLATE.package.clean``
~~~~~~~~~~~~~~~~~~~~~~~~~~

This state will remove the TEMPLATE package and has a depency on
``TEMPLATE.config.clean`` via include list.

``TEMPLATE.subcomponent``
~~~~~~~~~~~~~~~~~~~~~~~~

*Meta-state (This is a state that includes other states)*.

This state installs a subcomponent configuration file before
configuring and starting the TEMPLATE service.

``TEMPLATE.subcomponent.config``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This state will configure the TEMPLATE subcomponent and has a
dependency on ``TEMPLATE.config`` via include list.

``TEMPLATE.subcomponent.config.clean``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This state will remove the configuration of the TEMPLATE subcomponent
and reload the TEMPLATE service by a dependency on
``TEMPLATE.service.running`` via include list and ``watch_in``
requisite.

Testing
-------

Linux testing is done with ``kitchen-salt``.

Requirements
^^^^^^^^^^^^

* Ruby
* Docker

.. code-block:: bash

   $ gem install bundler
   $ bundle install
   $ bin/kitchen test [platform]

Where ``[platform]`` is the platform name defined in ``kitchen.yml``,
e.g. ``debian-9-2019-2-py3``.

``bin/kitchen converge``
^^^^^^^^^^^^^^^^^^^^^^^^

Creates the docker instance and runs the ``TEMPLATE`` main state, ready for testing.

``bin/kitchen verify``
^^^^^^^^^^^^^^^^^^^^^^

Runs the ``inspec`` tests on the actual instance.

``bin/kitchen destroy``
^^^^^^^^^^^^^^^^^^^^^^^

Removes the docker instance.

``bin/kitchen test``
^^^^^^^^^^^^^^^^^^^^

Runs all of the stages above in one go: i.e. ``destroy`` + ``converge`` + ``verify`` + ``destroy``.

``bin/kitchen login``
^^^^^^^^^^^^^^^^^^^^^

Gives you SSH access to the instance for manual testing.
