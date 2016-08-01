# Terraform provider for XenServer

## Dependencies

    go get 'github.com/hashicorp/terraform'
    go get 'github.com/amfranz/go-xen-api-client'
    go get 'github.com/amfranz/go-xmlrpc-client'

### Usage example

#### Provider configuration
```
provider "xenserver" {
  url = "<xen-server-url>"
  username = "<user-name>"
  password = "<password>"
}
```
Arguments:
 * url - URL to XenServer
 * username - XenServer user allowed to execute APIs
 * password - user password

#### VM Creation
```
resource "xenserver_vm" "web" {
    name_label = "web"
    base_template_name = "<desired template>"
    static_mem_min = 2048
    static_mem_max = 2048
    dynamic_mem_min = 2048
    dynamic_mem_max = 2048
    boot_order = "cdn"
    network_interface {
        network_uuid = "<uuid>"
        mac = "<desired-mac>"
        mtu = 1500
        device = 0
    }
    network_interface {
        network_uuid = "<uuid>"
        mtu = 1500
        device = 1
    }
    vcpus = 2
}
```
Arguments:
  * name_label - VM name
  * base_template_name - VM template
  * vcpus - Number of CPU's
  * static_mem_min - Minimal static memory
  * static_mem_max - Maximal static memory
  * dynamic_mem_min - Minimal dynamic memory
  * dynamic_mem_max - Maximal dynamic memory
  * boot_order (optional) - boot order. Use c for first bootable hard drive, d for CD-ROM, n for netboot. Example: cdn - boot from HD, CD, Network
  * network_interface (optional) - Array of network interface definitions
  * hard_drives (optional) - TBD
  * boot_parameters (optional) - TBD
  * installation_media_type (optional) - TDB
  * installation_media_location (optional) - TBD
  * cores_per_socket (optional) - TBD
  * xenstore_data (optional) - Extra VM configuration data for in-VM use

Network interface schema:
  * network_uuid - Network UUID. Required either network name of network uuid
  * mac - Desired mac address
  * mtu - MTU
  * device - interface order