# dnsenum

Dnsenum is a multithreaded perl script to enumerate DNS information of a domain and to discover non-contiguous ip blocks. The main purpose of Dnsenum is to gather as much information as possible about a domain. The program currently performs the following operations:

1. Get the host’s addresses (A record).
2. Get the namservers (threaded).
3. Get the MX record (threaded).
4. Perform axfr queries on nameservers and get BIND versions(threaded).
5. Get extra names and subdomains via google scraping (google query = “allinurl: -www site:domain”).
6. Brute force subdomains from file, can also perform recursion on subdomain that have NS records (all threaded).
7. Calculate C class domain network ranges and perform whois queries on them (threaded).
8. Perform reverse lookups on netranges (C class or/and whois netranges) (threaded).
9. Write to domain_ips.txt file ip-blocks.

This program is useful for pentesters, ethical hackers and forensics experts. It also can be used for security tests.

**Usage**: `dnsenum [Options] <domain>`

## Usage example

Don’t do a reverse lookup (`–noreverse`) and save the output to a file (`-o mydomain.xml`) for the domain `example.com`

**command** : `dnsenum --noreverse -o mydomain.xml example.com`

## [Options]:

Note: If no `-f` tag supplied will default to `/usr/share/dnsenum/dns.txt` or the `dns.txt` file in the same directory as `dnsenum.pl`

### GENERAL OPTIONS:

| Options | information
| ---                   | --- 
|`--dnsserver <server>` | Use this DNS server for A, NS and MX queries.
|`--enum`               | Shortcut option equivalent to `--threads 5 -s 15 -w`.|
| `-h`, `--help`        | Print this help message.
|`--noreverse`          |Skip the reverse lookup operations.
|`--nocolor`            |Disable ANSIColor output.
|`--private`            |Show and save private ips at the end of the file domain_ips.txt.
|`--subfile <file>`     |Write all valid subdomains to this file.
|`-t`, -`-timeout <value>`|The tcp and udp timeout values in seconds (default: 10s).
|`--threads <value>`    |The number of threads that will perform different queries.
|`-v`, `--verbose`      |Be verbose: show all the progress and all the error messages.

### GOOGLE SCRAPING OPTIONS:
| Options | information
| ---                   | --- 
|`-p`, `--pages <value>`|The number of google search pages to process when scraping names, the default is 5 pages, the -s switch must be specified.
|`-s`, `--scrap <value>` |The maximum number of subdomains that will be scraped from Google (default 15).

### BRUTE FORCE OPTIONS:
| Options | information
| ---                   | --- 
|`-f`, `--file <file>`  |Read subdomains from this file to perform brute force. (Takes priority over default dns.txt)
|`-u`, `--update  <a\|g\|r\|z>`|Update the file specified with the -f switch with valid subdomains. <br/>`a (all)` Update using all results. <br/>`g` Update using only google scraping results. <br/> `r` Update using only reverse lookup results. <br/>`z` Update using only zonetransfer results.
|`-r`, `--recursion`    |Recursion on subdomains, brute force all discovered subdomains that have an NS record.

### WHOIS NETRANGE OPTIONS:
| Options | information
| ---                   | --- 
|`-d`, `--delay <value>`  | The maximum value of seconds to wait between whois queries, the value is defined randomly, default: 3s.
|`-w`, `--whois`         | Perform the whois queries on c class network ranges. <br/> **Warning**: this can generate very large netranges and it will take lot of time to perform reverse lookups.

### REVERSE LOOKUP OPTIONS:
| Options | information
| ---                   | --- 
|`-e`, -`-exclude <regexp>` | Exclude PTR records that match the regexp expression from reverse lookup results, useful on invalid hostnames.

### OUTPUT OPTIONS:
| Options | information
| ---                   | --- 
|`-o --output <file>`     | Output in XML format. Can be imported in MagicTree (www.gremwell.com)
