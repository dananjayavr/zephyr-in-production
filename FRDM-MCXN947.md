Board info: https://docs.zephyrproject.org/latest/boards/nxp/frdm_mcxn947/doc/index.html

Use this to flash + run: 

`west flash -r linkserver`

Example workflow: 

`west build -b frdm_mcxn947/mcxn947/cpu0 my_app --pristine`
`west flash -r linkserver`