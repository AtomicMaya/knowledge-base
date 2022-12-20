# nmap

Base syntax: `nmap [type] [options] $IP`

Scan types:

- `sS`: TCP SYN/ACK or Stealth Scan

Options:

- `v|vv`: Increase verbosity
- `sV`: Service & Version detection
- `O`: OS detection
- `p[start[-end]]`: Specify port ranges
- `T[1|2|3|4|5]`: Scan timing (read: agressiveness)

## Example usages

- `nmap -v -A scanme.nmap.org`
