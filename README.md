### Server Node Installation :

#### 1. Run the installer

`curl -sfL https://get.rke2.io | sh -
`

#### 2. Enable the rke2-server service

`systemctl enable rke2-server.service
`

#### 3. Start the service

`systemctl start rke2-server.service
`

#### 4. Follow the logs, if you like

`journalctl -u rke2-server -f
`

#### 5: Some Important Thing That You Should Pay Attention

1: The `rke2-server` service will be installed. The `rke2-server` service will be configured to automatically restart after node reboots or if the process crashes or is killed.

2: Additional utilities will be installed at `/var/lib/rancher/rke2/bin/`. They include: kubectl, crictl, and ctr. Note that these are not on your path by default.

3: Two cleanup scripts, rke2-killall.sh and rke2-uninstall.sh, will be installed to the path at:

- `/usr/local/bin` for regular file systems
- `/opt/rke2/bin` for read-only and brtfs file systems
- `INSTALL_RKE2_TAR_PREFIX/bin` if `INSTALL_RKE2_TAR_PREFIX` is set

4: A kubeconfig file will be written to `/etc/rancher/rke2/rke2.yaml`

5: A token that can be used to register other server or agent nodes will be created at `/var/lib/rancher/rke2/server/node-token`

### Linux Agent (Worker) Node Installation

#### 1. Run the installer

`curl -sfL https://get.rke2.io | INSTALL_RKE2_TYPE="agent" sh -
`

#### 2. Enable the rke2-agent service

`systemctl enable rke2-agent.service
`

#### 3. Configure the rke2-agent service

`mkdir -p /etc/rancher/rke2/
`

`vim /etc/rancher/rke2/config.yaml`

#### Content for config.yaml:

```
server: https://<serverIP>:9345
token: <token from server node>
```

#### 4. Start the service

`systemctl start rke2-agent.service
`

#### Follow the logs, if you like

`journalctl -u rke2-agent -f`

#### Note:

Each machine must have a unique hostname. If your machines do not have unique hostnames, set the node-name parameter in the `config.yaml` file and provide a value with a valid and unique hostname for each node.
