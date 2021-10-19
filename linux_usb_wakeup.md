```
#!/bin/bash

################################################################################
function run_cmd() {
################################################################################
  echo "  $@"
  eval "$@"
}

# Disable USB wakeup.

for DEV in EHC{1,2} XHC; do
  grep -q "^${DEV}.*\*enabled" /proc/acpi/wakeup || continue
  run_cmd "echo ${DEV} > /proc/acpi/wakeup"
done
```
