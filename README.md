ansible-role-nrpe-plugins
=========

[![Build Status](https://travis-ci.org/CSC-IT-Center-for-Science/ansible-role-collectd-plugins.svg?branch=master)](https://travis-ci.org/CSC-IT-Center-for-Science/ansible-role-collectd-plugins)

This is not a place where to store collectd plugins. It can:

 - get_url of a remote file (and check checksum)
 - copy of a local file, perhaps available in files/
 - configre the plugin if it's a python plugin or run through exec

Requirements
------------

a list of checks


Role Variables
--------------

Example for setting up an iostat exec and some ceph python check copied from the ansible repo:
<pre>
collectd_plugin_exec_plugins:
  - { path: "../files/iostat_collectd_plugin.rb", name: "iostat_collectd_plugin.rb", user: "nobody:nobody", command: "/usr/local/collectd/plugins/iostat_collectd_plugin.rb" }

collectd_plugin_python_plugins:
  - { path: "../files/ceph_collectd/__init__.py", directory: "ceph", name: "__init__.py" }
  - { path: "../files/ceph_collectd/base.py", directory: "ceph", name: "base.py" }
  - { path: "../files/ceph_collectd/ceph_latency_plugin.py", directory: "ceph", name: "ceph_latency_plugin.py", import: "ceph_latency_plugin",  module_config: [ { key: "Verbose", value: "True" }, { key: "Cluster", value: "ceph" }, { key: "Interval", value: "60" }] }
  - { path: "../files/ceph_collectd/ceph_monitor_plugin.py", directory: "ceph", name: "ceph_monitor_plugin.py", import: "ceph_monitor_plugin",  module_config: [ { key: "Verbose", value: "True" }, { key: "Cluster", value: "ceph" }, { key: "Interval", value: "60" }]  }
  - { path: "../files/ceph_collectd/ceph_osd_plugin.py", directory: "ceph", name: "ceph_osd_plugin.py", import: "ceph_osd_plugin",  module_config: [ { key: "Verbose", value: "True" }, { key: "Cluster", value: "ceph" }, { key: "Interval", value: "60" }] }
  - { path: "../files/ceph_collectd/ceph_pg_plugin.py", directory: "ceph", name: "ceph_pg_plugin.py", import: "ceph_pg_plugin",  module_config: [ { key: "Verbose", value: "True" }, { key: "Cluster", value: "ceph" }, { key: "Interval", value: "60" }] }
  - { path: "../files/ceph_collectd/ceph_pool_plugin.py", directory: "ceph", name: "ceph_pool_plugin.py", import: "ceph_pool_plugin",  module_config: [ { key: "Verbose", value: "True" }, { key: "Cluster", value: "ceph" }, { key: "Interval", value: "60" }, { key: "TestPool", value: "test" } ]  }
</pre>

Dependencies
------------

https://github.com/CSC-IT-Center-for-Science/ansible-role-collectd

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: ansible-role-collectd }
         - { role: ansible-role-collectd-plugins }

License
-------

MIT

Author Information
------------------
