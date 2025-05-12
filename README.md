## Setup

Create hooks

### Hooks
change the command `dmesg` or include params. Create `plymouth-logcat` at `/etc/initcpio/hooks/`
```
#!/bin/bash

run_hook() {
    # Redirect boot messages to Plymouth
    exec >/dev/kmsg 2>&1
    plymouth_message_loop() {
        while read -r line; do
            plymouth update --status="$line"
        done
    }
    dmesg -w | plymouth_message_loop &
}
```

### Install 
create plymouth-log at `/etc/initcpio/install/`
```
#!/bin/bash

build() {
    add_runscript
}
```

#### Add
HOOKS=(...plymouth plymouth-log ...)

