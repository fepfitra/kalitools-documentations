# dnsrecon

DNSRecon is a Python script that provides the ability to perform:
1. Check all NS Records for Zone Transfers.
2. Enumerate General DNS Records for a given Domain (MX, SOA, NS, A, AAAA, SPF and TXT).
3. Perform common SRV Record Enumeration.
4. Top Level Domain (TLD) Expansion.
5. Check for Wildcard Resolution.
6. Brute Force subdomain and host A and AAAA records given a domain and a wordlist.
7. Perform a PTR Record lookup for a given IP Range or CIDR.
8. Check a DNS Server Cached records for A, AAAA and CNAME
9. Records provided a list of host records in a text file to check.
10. Enumerate Hosts and Subdomains using Google

**usage**: `dnsrecon.py [-h] [-d DOMAIN] [-n NS_SERVER] [-r RANGE] [-D DICTIONARY] [-f] [-a] [-s] [-b] [-y] [-k] [-w] [-z] [--threads THREADS] [--lifetime LIFETIME] [--tcp] [--db DB] [-x XML] [-c CSV] [-j JSON] [--iw] [--disable_check_recursion] [--disable_check_bindversion] [-V] [-v] [-t TYPE]`

## Usage example
Scan a domain (`-d example.com`), use a dictionary to brute force hostnames (`-D /usr/share/wordlists/dnsmap.txt`), do a standard scan (`-t std`), and save the output to a file (`–xml dnsrecon.xml`)

**command** : `dnsenum --noreverse -o mydomain.xml example.com`
## options:

| Options | information
| ---                   | --- 
| `-h`, `--help`            |show this help message and exit
| `-d DOMAIN`, `--domain DOMAIN`| Target domain.
  `-n NS_SERVER`, `--name_server NS_SERVER` |Domain server to use. If none is given, the SOA of the target will be used. Multiple servers can be specified using a comma separated list.
|`-r RANGE`, `--range RANGE`|IP range for reverse lookup brute force in formats   (first-last) or in (range/bitmask).
| `-D DICTIONARY`, `--dictionary DICTIONARY` | Dictionary file of subdomain and hostnames to use for brute force.
  `-f`                    |Filter out of brute force domain lookup, records that resolve to the wildcard defined IP address when saving records.
  `-a`                    |Perform AXFR with standard enumeration.
  `-s`                    |Perform a reverse lookup of IPv4 ranges in the SPF record with standard enumeration.
  `-b`                    |Perform Bing enumeration with standard enumeration.
  `-y`                    |Perform Yandex enumeration with standard enumeration.
  `-k`                    |Perform crt.sh enumeration with standard enumeration.
  `-w`                    |Perform deep whois record analysis and reverse lookup of IP ranges found through Whois when doing a standard enumeration.
  `-z`                    |Performs a DNSSEC zone walk with standard enumeration.
  `--threads THREADS`     |Number of threads to use in reverse lookups, forward lookups, brute force and SRV record enumeration.
  `--lifetime LIFETIME`   |Time to wait for a server to respond to a query. default is 3.0
  `--tcp`                 |Use TCP protocol to make queries.
  `--db DB`               |SQLite 3 file to save found records.
  `-x XML`, `--xml XML`     |XML file to save found records.
  `-c CSV`, `--csv CSV`     |Save output to a comma separated value file.
  `-j JSON`, `--json JSON`  |save output to a JSON file.
  `--iw`                  |Continue brute forcing a domain even if a wildcard record is discovered.
  `--disable_check_recursion`                        |Disables check for recursion on name servers
  `--disable_check_bindversion`|Disables check for BIND version on name servers
  `-V`, `--version`         |Show DNSrecon version
  `-v`, `--verbose`         |Enable verbose
  `-t TYPE`, `--type TYPE`  |Type of enumeration to perform. <br/> Possible types: <br> &nbsp; &nbsp; &nbsp; `std`:      SOA, NS, A, AAAA, MX and SRV. <br> &nbsp; &nbsp; &nbsp; `rvl`:      Reverse lookup of a given CIDR or IP range.<br> &nbsp; &nbsp; &nbsp; `brt`:      Brute force domains and hosts using a given dictionary.<br> &nbsp; &nbsp; &nbsp; `srv`:      SRV records.<br> &nbsp; &nbsp; &nbsp; `axfr`:     Test all NS servers for a zone transfer.<br> &nbsp; &nbsp; &nbsp; `bing`:     Perform Bing search for subdomains and hosts.<br> &nbsp; &nbsp; &nbsp; `yand`:     Perform Yandex search for subdomains and hosts.<br> &nbsp; &nbsp; &nbsp; `crt`:      Perform crt.sh search for subdomains and hosts.<br> &nbsp; &nbsp; &nbsp; `snoop`:    Perform cache snooping against all NS servers for a given domain, testing all with file containing the domains, file given with `-D` option.<br> &nbsp; &nbsp; &nbsp; `tld`:      Remove the TLD of given domain and test against all TLDs registered in IANA.<br> &nbsp; &nbsp; &nbsp; `zonewalk`: Perform a DNSSEC zone walk using NSEC records. 