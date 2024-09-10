## BIOS

TODO: Add notes from Dropbox

Push F12 to select boot device

## SSD Over provisoning

### NVME name spacing (not possible)

According to this page: https://stackoverflow.com/questions/74985043/how-i-do-nvme-overprovisioning

The `WD_BLACK SN850X 1000GB` NVME drive does not support NVME namespaces.

`nn` returns `1`.

### Crappy over provisioning

Create a 70GB unused partition.

(See partitioning for further details)
