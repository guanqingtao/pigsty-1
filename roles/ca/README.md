# CA (ansible role)

This role will provied a usable CA key & cert



### Tasks

[tasks/main.yml](tasks/main.yml)

```yaml
Check for existing consul		  TAGS: [consul_check]
Consul exists flag fact set		  TAGS: [consul_check]
Abort due to consul exists		  TAGS: [consul_check]
Clean existing consul instance	  TAGS: [consul_check]
Purge existing consul instance	  TAGS: [consul_check]
Make sure consul is installed	  TAGS: [consul_install]
Get dcs server node names		  TAGS: [consul_config]
Get dcs node name from var		  TAGS: [consul_config]
Fetch hostname as dcs node name	  TAGS: [consul_config]
Get dcs name from hostname		  TAGS: [consul_config]
Copy /etc/consul.d/consul.json	  TAGS: [consul_config]
Get dcs bootstrap expect quroum	  TAGS: [consul_server]
Copy consul server service unit	  TAGS: [consul_server]
Launch consul server service	  TAGS: [consul_server]
Wait for consul server online	  TAGS: [consul_server]
Copy consul agent service		  TAGS: [consul_agent]
Launch consul agent service		  TAGS: [consul_agent]
Wait for consul agent online	  TAGS: [consul_agent]
```

### Default variables

[defaults/main.yml](defaults/main.yml)

```yaml
dcs_type:    consul                               # default dcs server type: consul
dcs_servers: []                                   # default dcs servers
dcs_purge: false                                  # force remove existing server
# dcs_check_interval: 15s                         # default service check interval (not used)
# dcs_check_timeout:  3s                          # default service check timeout  (not used)
```