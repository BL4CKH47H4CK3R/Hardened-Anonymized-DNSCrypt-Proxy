<h1 align="center"><a href=https://github.com/BL4CKH47H4CK3R/Hardened-Anonymized-DNSCrypt-Proxy>Hardened-Anonymized-DNSCrypt-Proxy</a></h1>
<p align=center>Wipe Snoopers Out Of Your Networks</p>

A flexible DNS proxy, with support for modern encrypted DNS protocols such as [DNSCrypt v2](https://dnscrypt.info/protocol), [DNS-over-HTTPS](https://www.rfc-editor.org/rfc/rfc8484.txt), [Anonymized DNSCrypt](https://github.com/DNSCrypt/dnscrypt-protocol/blob/master/ANONYMIZED-DNSCRYPT.txt) and [ODoH (Oblivious DoH)](https://github.com/DNSCrypt/dnscrypt-resolvers/blob/master/v3/odoh-servers.md).


## Features

- For all features please refer to the [OFFICIAL PAGE](https://github.com/DNSCrypt/dnscrypt-proxy#features)
- All binary files are downloaded from the [OFFICIAL RELEASE PAGE](https://github.com/DNSCrypt/dnscrypt-proxy/releases)


## Why This Project ?

There Are Automated DNSCrypt-Proxy Client For Both [Windows](https://github.com/bitbeans/SimpleDnsCrypt) & [Android (Magisk Module)](https://github.com/d3cim/dnscrypt-proxy-android) <br/>
But For Linux, People Find It Hard To Configure DNSCrypt-Proxy Manually. But I Wanted To Keep It Simple, So It's Here !


## Supported Linux Distributions

`Arch / Arch Based Distro With SystemD & NetworkManager`


## Differences From The Main DNSCrypt-Proxy Project

- `server_names` = `ams-dnscrypt-nl` [NLD], `d0wn-tz-ns1` [TZA], `dct-nl` [NLD], `dct-ru` [RUS], `dnscrypt.be` [BEL], `dnscrypt.pl` [POL], `dnscrypt.uk-ipv4` [GBR], `dnswarden-uncensor-dc-swiss` [CHE], `meganerd` [NLD], `openinternet` [USA], `plan9dns-fl` [USA], `plan9dns-mx` [MEX], `plan9dns-nj` [USA], `pryv8boi` [DEU], `sby-limotelu` [IDN], `scaleway-ams` [NLD], `scaleway-fr` [FRA], `serbica` [NLD], `techsaviours.org-dnscrypt` [DEU], `v.dnscrypt.uk-ipv4` [GBR] are the resolvers in use.

- `doh_servers = false` (disable servers implementing the `DNS-over-HTTPS` protocol)

- `require_dnssec = true` (server must support `DNSSEC` security extension)

- `force_tcp = true` (fix for mobile data intial connection random issues if `routes` have been set and `skip_incompatible = true`, see [DNSCrypt/dnscrypt-proxy/discussions/2020](https://github.com/DNSCrypt/dnscrypt-proxy/discussions/2020))

- `timeout = 1000` (set the max. response time of a single DNS query from `5000` to `1000` ms.)

- `blocked_query_response = 'refused'` (set `refused` response to blocked queries)

- `# log_level = 0` (set the log level of the `dnscrypt-proxy.log` file to very verbose, but keep it disabled by default)

- `dnscrypt_ephemeral_keys = true` (create a new, unique key for every single DNS query)

- `bootstrap_resolvers = ['45.11.45.11:53']` (use [DNS.SB](https://dns.sb/) instead [CloudFlare](https://archive.today/tS1Ln))

- `netprobe_address = '45.11.45.11:53'` (use [DNS.SB](https://dns.sb/) instead [CloudFlare](https://archive.today/tS1Ln))

- `block_ipv6 = true` (immediately respond to IPv6-related queries with an empty response)

- `blocked-names.txt`, `blocked-ips.txt`, `allowed-names.txt` and `allowed-ips.txt` files enabled. (to know more specifics about this, please refer to the [Filters (optional)](https://github.com/d3cim/dnscrypt-proxy-android#filters-optional) section below)

- `anonymized_dns` feature enabled. (`routes` are indirect ways to reach DNSCrypt servers, each resolver has 2 relays assigned)

- `skip_incompatible = true` (skip resolvers incompatible with anonymization instead of using them directly)

- `direct_cert_fallback = false` (prevent direct connections through the resolvers for failed certificate retrieved via relay)


## Configure [Copy-Paste]

    git clone https://github.com/BL4CKH47H4CK3R/Hardened-Anonymized-DNSCrypt-Proxy
    cd Hardened-Anonymized-DNSCrypt-Proxy
    makepkg -Ccrfs --noconfirm
    sudo pacman -U *zst


## Deconfigure [Copy-Paste]

    sudo pacman -Rcnsu Hardened-Anonymized-DNSCrypt-Proxy


## Filters [Optional]

Filters are a powerful set of built-in features, that let you control exactly what domain names and IP addresses your device are allowed to connect to. This can be used to block ads, trackers, malware, or anything you don't want your device to load.
To know more about it, you can check the official documentation [DNSCrypt-Proxy-Filters](https://github.com/DNSCrypt/dnscrypt-proxy/wiki/Filters)


## DNS Leak Testing [Websites]

- [IPLeak](https://ipleak.net)
- [DNSLeakTest](https://www.dnsleaktest.com)
- [BrowserLeaks](https://browserleaks.com/dns)


## Configuration [Post Installing]

- You can edit `dnscrypt-proxy.toml` as you wish located on `/etc/dnscrypt-proxy/dnscrypt-proxy.toml`
- For more detailed configuration please refer to [official documentation](https://github.com/DNSCrypt/dnscrypt-proxy/wiki/Configuration)


## Credits

- [Frank Denis](https://github.com/jedisct1) & All Other Contributors
For This Awesome [Project](https://github.com/DNSCrypt/dnscrypt-proxy)
- Special Thanks To [d3cim](https://github.com/d3cim) For The DNSCrypt-Proxy [Configuration](https://github.com/d3cim/dnscrypt-proxy-android/raw/master/config/dnscrypt-proxy.toml)
