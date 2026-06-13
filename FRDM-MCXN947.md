Board info: https://docs.zephyrproject.org/latest/boards/nxp/frdm_mcxn947/doc/index.html

Use this to flash + run: 

`west flash -r linkserver`

Example workflow: 

`west build -b frdm_mcxn947/mcxn947/cpu0 my_app --pristine`

`west flash -r linkserver`

Custom Board: 

`west build -b training/mcxn947/cpu0 app --pristine`

Using sysbuild (combining both bootloader + app and flash it in single step): 

`west build -b training/mcxn947/cpu0 app --sysbuild -d build/sysboot --pristine`
`west flash -r linkserver -d build/sysboot`

Note for MCXA153: 

Q: I am on an MCXA153 io MCXA156. It has only 128K. The partitions are defined in board DTS, but when building, the binary does not fit into them. So I guess MCUBoot is applicable starting from 256K..

A: Tweak configuration (of MCUboot) to save space (?)

Extract public key 

`imgtool getpub -k keys/my-key.pem -e pem`

Tips for speeding up CI job: 
 - cache container
 - use ccache
 - use own machine (wired to GH Actions)

Release build: 

`west build -b training/mcxn947/cpu0 app --sysbuild -d build/release --pristine -S release`
`west flash -r linkserver -d build/release`

Hardening audit: 

`west build -b training/mcxn947/cpu0 -d build/release/app -S release app -t hardenconfig`

This compares the recommended project config against one got compiled, and test FAIL based on that