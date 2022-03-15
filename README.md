# lkddb-query

This is a small hacked together script that will parse the [LKDDb database](https://cateee.net/lkddb/) and print the kernel configuration details to `stdout` 

This was created to have a quick way to easily get the definition for a specific Linux kernel configuration option on the command line

## Clone

```
git clone --recurse-submodules https://github.com/droogie/lkddb-query
```

## Usage

```
$ ./lkddb-query -h                          
usage: lkddb-query [-h] config_var

Parse an LKDDb for a specific Linux Kernel configuration option for details

positional arguments:
  config_var  Example: CONFIG_DEFAULT_MMAP_MIN_ADDR

options:
  -h, --help  show this help message and exit
```

```
$ ./lkddb-query CONFIG_DEFAULT_MMAP_MIN_ADDR
CONFIG_DEFAULT_MMAP_MIN_ADDR: Low address space to protect from user allocation

This is the portion of low virtual memory which should be protected
from userspace allocation.  Keeping a user from writing to low pages
can help reduce the impact of kernel NULL pointer bugs.

For most ia64, ppc64 and x86 users with lots of address space
a value of 65536 is reasonable and should cause no problems.
On arm and other archs it should not be higher than 32768.
Programs which use vm86 functionality or have some need to map
this low address space will need CAP_SYS_RAWIO or disable this
protection by setting the value to 0.

This value can be changed after boot using the
/proc/sys/vm/mmap_min_addr tunable.
```

## LKDDb 

LKDDb (Linux Kernel Driver DataBase) is an attempt to build a comprensive database of hardware and protocols know by Linux kernels. The driver database includes numeric identifiers of hardware, the kernel configuration menu needed to build the driver and the driver filename. The database is build automagically from kernel sources, so it is very easy to have always the database updated.

The database provided in this repository was generated against [Linux 5.17-rc8](https://github.com/torvalds/linux/commit/09688c0166e76ce2fb85e86b9d99be8b0084cdf9). Refer to the [llkdb repository](https://github.com/cateee/lkddb) for instructions on building a new database. This script is essentially a stripped down version of  [gen-web-lkddb.py](https://github.com/cateee/lkddb/blob/master/gen-web-lkddb.py) but simply prints the description and help text for whichever configuration option queried. 

