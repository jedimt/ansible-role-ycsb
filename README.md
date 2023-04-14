Ansible Role: YCSB
=========

Installs YCSB for MongoDB or Cassandra

Requirements
------------

None.

Role Variables
--------------

There are three variables included in the role:

    # Number of threads to use when loading the database - for the example ycsb_load_db.sh file
    ycsb_load_threads: 12

    # Number of threads to use when running a workload - for the example ycsb_run_workload.sh file
    ycsb_run_threads: 12

    # dbsize is in # of records. Each record is ~1167 bytes.
    # This is fed to YCSB ycsb_load_db.sh script for creating the database
    # records = target db size in bytes / 1167
    # Examples:
    # ~1TB =    (1000000000000 Bytes / 1167 bytes per record) = 856898029 records
    # ~500GB =  (500000000000 Bytes / 1167 bytes per record)  = 428449014 records
    # ~100GB =  (100000000000 Bytes / 1167 bytes per record)  = 85689802 records
    # ~30GB =   (30000000000 Bytes / 1167 bytes per record)   = 25706940 records
    dbsize: 85689802

    # Indicate which YCSB bindings to install (mongodb|casandra)
    ycsb_bindings: 'cassandra'

Dependencies
------------

None

Example Playbook
----------------

    # ===========================================================================
    # Install YCSB
    # ===========================================================================
    - name: Install YCSB
      hosts: localhost
      connection: local
      gather_facts: false
      become: false

      roles:
        - { role: jedimt.ycsb,
            dbsize: 85689802,
            ycsb_load_threads: 8,
            ycsb_run_threads: 12,
            ycsb_bindings: 'cassandra'
        }

License
-------

MIT

Author Information
------------------

Aaron Patten
aaronpatten@gmail.com
