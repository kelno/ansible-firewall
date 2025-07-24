# Usage

Make other roles depend on this one with:  
```
dependencies:
  - role: firewall
    vars:
      _firewall_register_rules:
        - port: 8096 # Only port is mandatory, the rest will use default values allow TCP (from everywhere)
        - protocol: udp
          port: 1900
          rule: allow
        - protocol: tcp
          port: 1901
          rule: allow
          from_ip: 192.168.1.0/24
```

Then you need to apply those rules, for example from main playbook:  
```
- name: Install & apply accumulated firewall rules
  hosts: all
  roles:
    - role: firewall
      tasks_from: apply

```


Old doc:  
```
_firewall_register_rules:
        type: list
        elements: dict
        required: false
        description: List of firewall rules added by other roles
        options:
          port:
            type: int
            required: true
            description: Port number to configure
          protocol:
            type: str
            required: false
            choices: ["tcp", "udp"]
            description: Protocol (tcp or udp)
            default: "tcp"
          rule:
            type: str
            required: false
            choices: ["allow", "deny", "reject", "limit"]
            description: UFW rule action
            default: "allow"
          from_ip:
            type: str
            required: false
            description: Source network in CIDR notation (e.g. 192.168.0.0/16)
            default: None
```
