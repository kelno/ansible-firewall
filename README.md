# Usage

Make your role depend on this one.

`meta/main.yml`
```yml
dependencies:
  - role: firewall
```

Add your custom rules as a file to include in nftable.d, in the relevant chain.
Currently supported chains are listed in vars/main.yml, providing dir variables you should use to place your file.

Example would be to create a file `{{ firewall_nftables_extra_config_inet_input_dir}}/web_main.nft`

with content:
```yaml
tcp dport {{ web_main_public_port }} ip accept
```
