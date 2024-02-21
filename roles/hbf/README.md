**hbf**
=========

Deploying the **H**ost**B**ase**F**irewall-agent on a host.

Role Handlers
--------------
| Handler Name               | Description                   | Condition                                                 |
|----------------------------|-------------------------------|-----------------------------------------------------------|
| restart {{ service_name }} | Restart the specific service. | Service {{ service_name }} configuration file is updated. |
| reboot:shutdown            | Restart the host.             | After installing ndpi module (`hbf_ndpi_enabled: true`).  |


Role Variables
--------------

| Variable Name                                      | Description                                                                                                        | Type    |
|----------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|---------|
| `hbf_server.extapi.address`                        | IP address of the HBF server                                                                                       | string  |
| `hbf_server.extapi.port`                           | Port utilized by the HBF server for communication.                                                                 | string  |
| `hbf_server.rules.extra`                           | Ip addresses of highly critical services that require constant access.                                             | list    |
| `hbf_base_rules`                                   | Combination of `hbf.rules.dns_servers` and `hbf.rules.extra`.                                                      | list    |
| `hbf_nft_exporter.port`                            | Port on which the [nftables-exporter](https://github.com/H-BF/nftables-exporter) will operate. By default: *9630*. | string  |
| `hbf_nft_exporter.endpoint`                        | Endpoint for the [nftables-exporter](https://github.com/H-BF/nftables-exporter). By default: */metrics*.           | string  |
| `swarm_base_path`                                  | Base directory for installing HBF components. By default: */opt/swarm*.                                            | string  |
| `hbf_components.<component>.enabled`               | Boolean flag to install/uninstall the specified component.                                                         | boolean |
| `hbf_components.<component>.packages[].name`       | Name of the specified component package.                                                                           | string  |
| `hbf_components.<component>.packages[].version`    | Version of the specified component.                                                                                | string  |
| `hbf_components.<component>.packages[].from_github`| Indicates if the package needs to be downloaded from the [HBF organization repository](https://github.com/H-BF/).  | boolean |
| `hbf_components.<component>.packages[].github_url` | URL for downloading the package from the [HBF organization repository](https://github.com/H-BF/).                  | string  |
| `hbf_components.<component>.files[].src`           | Source path of the component configuration file.                                                                   | string  |
| `hbf_components.<component>.files[].dest`          | Destination path (on the host) of the component configuration file.                                                | string  |
| `hbf_components.<component>.service.name`          | Name of the service (on the host) provided by the component.                                                       | string  |
| `hbf_components.<component>.service.trigger[]`     | Action for the service after installing the component.                                                             | string  |


Role Variables defined in `main.yml`
--------------

| Variable Name                    | Description                                                                      | Type    |
|----------------------------------|----------------------------------------------------------------------------------|---------|
| `hbf_agent_enabled`              | Install/Uninstall the agent on the node.                                         | boolean |
| `hbf_agent_version`              | Version of the hbf-agent.                                                        | string  |
| `hbf_ndpi_enabled`               | Install/Uninstall the ndpi module for [swarm-nft](https://github.com/H-BF/nft).  | boolean |
| `hbf_ndpi_version`               | Version of [ndpi](https://github.com/H-BF/nDPI) module for swarm-nft.            | string  |
| `hbf_agent_fqdn_mode`            | Method of handling fqdn rules. Possible values: `dns`, `ndpi`, `combine`.        | string  |
| `hbf_swarm_nft_enabled`          | Install/Uninstall swarm-nft and swarm-libnftnl.                                  | boolean |
| `hbf_swarm_libnftnl_version`     | Version of [swarm-libnft](https://github.com/H-BF/libnftnl).                     | string  |
| `hbf_swarm_nft_version`          | Version of [swarm-nft](https://github.com/H-BF/nft).                             | string  |
| `hbf_nftables_exporter_version`  | Version of [nftables-exporter](https://github.com/H-BF/nftables-exporter).       | string  |