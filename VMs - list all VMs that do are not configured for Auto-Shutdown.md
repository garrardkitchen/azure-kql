#
# Imperfect KQL that lists all VMs that are not configured with Auto-Shutdown
#
resources
| where type == "microsoft.compute/virtualmachines"
| where name contains "<replace-partial-name-here>"
| join kind=leftouter  (
    resources 
    | where type == "microsoft.devtestlab/schedules"
    | project targetResourceId = tostring(properties.targetResourceId)) on $left.id == $right.targetResourceId
| project name, status=properties.extended.instanceView.powerState.displayStatus, targetResourceId
| where isempty(targetResourceId)