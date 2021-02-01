# Ansible Collection - mcen1.puppetdb_facts

Retrieve information from a Puppet DB instance using a query.

```
options:
    puppetdb_url:
        description: URL to the PuppetDB API. Typically https://puppet.company.com:8081/pdb/query/v4/inventory
        required: true
        type: str
    cert_file:
        description: Path to public key cert.
        required: false
        type: str
    pkey_file:
        description: Path to private key file.
        required: false
        type: str
    query_by:
        description: How to retrieve your host, ie: facts.hostname or certname. {"query":["=","$query_by","$query_equals"]}
        required: true
        type: str
    query_equals:
        description: What query_by should equal to, typically a server name. {"query":["=","$query_by","$query_equals"]}
        required: true
        type: str
    validate_certs:
        description: Whether or not to validate certs.
        required: false
        type: bool
```

Example:
```
  tasks:
    - name: Get puppet output
      mcen1.puppetdb_facts.puppetdbfacts:
        puppetdb_url: https://puppet.company.com:8081/pdb/query/v4/inventory
        cert_file: '{{puppetdb_public}}'
        pkey_file: '{{puppetdb_private}}'
        query_by: 'facts.hostname'
        query_equals: 'servername'
        validate_certs: no
      register: puppetfact
    - name: print debug
      debug:
        msg: "{{puppetfact}}"
```

Output:
```
ok: [127.0.0.1] => {
    "msg": {
        "changed": false,
        "failed": false,
        "message": "",
        "original_message": "",
        "output": [
            {
                "certname": "servername.company.com",
                "environment": "dev",
                "facts": {
                    "agent_specified_environment": "dev",
                    "aio_agent_version": "5.5.22",
                    "architecture": "x86_64",
           [...]
```

