# ansible-role-dhcpd-docker

Ansible role to configure and deploy a docker container for running isc dhcpd server.

# requirements
- ubuntu 18.04. It might work in other ubuntu versions but has been tested with ubuntu 18.04
- docker: Needs docker installed in the server


# Configuration Variables

```yaml
dhcpd_container_name: dhcpd # Chnage the docker container name
dhcpd_container_image: networkboot/dhcpd:latest # Image to be used
dhcpd_container_recreate: no # Wether the container should be recreated or not. Need to specify if there is a need to restart the container

dhcpd_bind_interface: eth1 # Interface where server will bind

dhcpd_config_dir: /data/dhcpd # Config dir on the host Also dhcpd.leases file will be here

# Global configs (if this options are not specified in the networks then the network will inherit the global ones)
dhcpd_global_domain_name: home.local # domain name
dhcpd_global_dns_servers: "8.8.8.8, 1.1.1.1" # Dns server separated by comma
dhcpd_global_default_lease_time: 7200 #2 hours Lease time
dhcpd_global_max_lease_time: 604800 #7 days maximun lease time
dhcpd_global_authoritative: yes # Wether the server will be autoritative for the subnet or not

# Here is were we define the networks the will server dhcp for.
# Needs at least 1 and it's mandatory
networks:
  - net_address: 192.168.2.0 # Mandatory subnet address
    netmask: 255.255.255.0 # Mandatory network mask
    range: "192.168.2.21 192.168.2.250" #Mandatory, range where dhcp will assing ip addresses
    gateway: 192.168.2.1 # Mandatory, Default gateway for the subnet
    dns_servers: "192.168.2.1" #Optional, Dns servers neets to be specified comma separated
    domain_name: home.local #Optional, Domain name for the subnet
    domain_search: '"home.local"' #Optional, Set domaine search need to be comma separated and enclosed in "" double quotes. Same format as the file expects.

static_hosts:
  - name: myhost # Mandatory, Hostname (must be unique)
    ip: 192.168.2.3 # Mandatory, Fixed IP address
    mac: ab:cd:ef:01:02:03 # Mandatory, Mac Address of the device

```


# Limitations
- Only supports on IPv4
- Runs as network mode host so network isolaiton is not possible

# To Do
- Make it work not only in network mode host
- add confoguration for lease times to a network


# Disclaimer

THE SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.