# ewc-playbooks
Playbooks to install pytroll processing and wms in the EWC

To create a podman secret (eg password):
```
systemd-ask-password -n | podman secret create pgpassword -
```
