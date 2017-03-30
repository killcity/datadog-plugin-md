Role: role-datadog-customchecks
=========

Role Scope
--------------
* install custom datadog integrations based on booleans in `main.yml`

Group Vars (Tower Inventory)
--------------
The following vars need to be populated from the inventory or optionally as runtime vars.

### Integration: mdraid
`has_mddevice: yes` enables the md raid custom integration. Since the majority of our boxes are using mdraid, the default is 'yes'.

Example:
```
has_mddevice: no
```

Runtime Vars
--------------
* none required - expects vars to be populated by tower inventory

Datadog Metrics
----------------

### Integration: mdraid

The information is inelegantly parsed from `/proc/mdstat` and sent to datadog
as various metrics.

## Gauges

 * `md_device.disk.total` The total number of disks that are supposed to be
   active in the array.
 * `md_device.disk.active` The number of disks that are active in the
   array.  i.e. non-failed and non-spare.  Disks that are considered recovering
   will be included in this count.
 * `md_device.disk.spare` The number of spare disks in the array.
 * `md_device.disk.failed` The number of failed disks in the array.
 * `md_device.disk.up` The total number of fully functioning disks in the
   array.  i.e. non-failed, non-spare and non-recovering.
 * `md_device.recovery.complete` The percentage of recovery completed.  Will
   return 100% for arrays that are not in recovery status.
 * `md_device.recovery.speed_bytes` The speed of recovery.  Will return 0 for
   arrays that are not in recovery status.

