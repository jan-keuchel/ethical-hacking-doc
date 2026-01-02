# Reconnaissance

## Easy to get information
- `whois <domain>`
    - Registrar WHOIS Server
    - Registrar URL
    - Record creation date
    - Reord update date
    - Registrant contact infp and address
    - Admin contact info and address
    - Tech contact info and address

- DNS Server querying
    - `nslookup <domain>`
        - Get Ip addresses of domain (A and AAAA)
    - `dig <domain>`
        - Get different servers (NS, MX, TXT, ...)
        - Reverse lookup with `dig -x <IP>`
    - `host <domain>`
        - Get IPv4 and IPv6 addresses
    - [ViewDNSInfo](https://viewdns.info/)
        - reverse lookup

- `traceroute <domain>`
    - Get the route of the packet from localhost to `<domain>`

## Google Foo

|Syntax                     | Function                      |
|---------------------------|-------------------------------|
| "something to search for" | Find results with exact search phrase|
| test filetype:pdf         | Find .pdf files relating the search term |
| test again site:<site>    | Find results from a specific <site> |
| test again -site:<site>   | Exclude results from a <site> |
| some phrase intitle:abc   | Find pages with specific term in the page title |
| another one inurl:keuchel | Find pages with speicific term in the page URL |

## Search engines and third party platforms
- [Threat Intelligence Platform](https://threatintelligenceplatform.com/)
    - Basic information
    - More detailed information about used resources
    - Potentially dangerous content
- [Censys Search](https://search.censys.io/)
    - IP and domain information

## recon-ng
- Start with `recon-ng`
- Create a workspace: `workspaces create <workspace-name>`
- Show database tables: `db schema`
- Insert a vaulue into a table: `db insert <table-name>`
- Marketplace
    - `marketplace search`: Get all available modules
    - `marketplace search <term>`: Search for something
    - `marketplace info <module>`: Get information of a module
    - `marketplace install <module>`
    - `marketplace remove <module>`
- Navigating Modules
    - `modules search`: List all installed modules
    - `modules search <term>`: Search for installed module
    - `modules load <module>`
    - `ctrl+c`: unload module
- Within a module
    - `options list`: Show all options of the selected module
    - `options set <option> <value>`
    - Keys
        - `keys list`
        - `keys add <key-name> <key-value>`
        - `keys remove <key-name>`
