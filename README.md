swap_file
=========

Creates a swap file

Requirements
------------

None

Role Variables
--------------

# swap_file_path

Full path for swap file

# swap_file_state [ present | absent ]

"present" creates the swap file, "absent" removes it

# swap_file_size

Size of swap file in human readable form. eg: 1M, 1G. Any value understood by filter "human_to_bytes"

# swap_file_priority [ -1 to 32767 ]

Priority for the swap file. "Higher values indicate higher priority". "man swapon"

# swap_file_show_btrfs_warn [ true | false ]

A warning will be displayed if working on a btrfs filesystem and
this variable is not set to false

When using btrfs, some operations such as snapshots will fail
on a subvolume while a swap file is active on said subvolume.
Consider creating a subvolume exclusively for the swap file
if you have not done so already.
https://btrfs.readthedocs.io/en/latest/Swapfile.html

Also note that if you deactivate a swapfile on btrfs and then
do a snapshot on the subvolume, you will no longer be able to
use the same swapfile as swap. You will have to create another
swapfile after the snapshot operation


Dependencies
------------

None

Example Playbook
----------------

    - hosts: servers
      vars:
        swap_file_path: '/swapfile'
        swap_file_state: 'present'
        swap_file_size: '2G'

      roles:
        - basicbind.swap_file

License
-------

GPL-3.0-only

Author Information
------------------
basicbind - https://github.com/basicbind
