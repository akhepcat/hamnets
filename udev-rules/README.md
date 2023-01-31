Place these files into /etc/udev/rules.d/

they'll ensure that your radios can always use a statically named device, rather than a dynamic USB tty name,
which could change during hotplug or reboot events.
