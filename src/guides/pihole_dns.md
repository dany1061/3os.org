title: Pi-hole on Ubuntu with DNS over HTTP
description: Pi-hole, DNS ads, tracking blocking on Ubuntu with DNS over HTTP, list of blacklist

<link rel="stylesheet" href="/assets/CSS/roundedCorners.css">

# Pi-hole as DNS Server with DNS over HTTPS

My Setup:

<div style="width:80%; margin:0 auto">
   <img src="/assets/images/guides/pi-hole/pi-hole_setup.jpg" alt="network flow">
</div>

Requirements

```bash
apt-get install curl
```

Debug

```bash
pihole -d
```

Blocklists:

- https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts
- https://mirror1.malwaredomains.com/files/justdomains
- http://sysctl.org/cameleon/hosts
- https://zeustracker.abuse.ch/blocklist.php?download=domainblocklist
- https://s3.amazonaws.com/lists.disconnect.me/simple_tracking.txt
- https://s3.amazonaws.com/lists.disconnect.me/simple_ad.txt
- https://hosts-file.net/ad_servers.txt
- https://dbl.oisd.nl/
- https://raw.githubusercontent.com/anudeepND/blacklist/master/adservers.txt
- https://raw.githubusercontent.com/hectorm/hmirror/master/data/adaway.org/list.txt
- https://raw.githubusercontent.com/hectorm/hmirror/master/data/adblock-nocoin-list/list.txt
- https://raw.githubusercontent.com/hectorm/hmirror/master/data/adguard-simplified/list.txt
- https://raw.githubusercontent.com/hectorm/hmirror/master/data/anudeepnd-adservers/list.txt
- https://raw.githubusercontent.com/hectorm/hmirror/master/data/disconnect.me-ad/list.txt
- https://raw.githubusercontent.com/hectorm/hmirror/master/data/disconnect.me-malvertising/list.txt
- https://raw.githubusercontent.com/hectorm/hmirror/master/data/disconnect.me-malware/list.txt
- https://raw.githubusercontent.com/hectorm/hmirror/master/data/disconnect.me-tracking/list.txt
- https://raw.githubusercontent.com/hectorm/hmirror/master/data/easylist/list.txt
- https://raw.githubusercontent.com/hectorm/hmirror/master/data/easyprivacy/list.txt
- https://raw.githubusercontent.com/hectorm/hmirror/master/data/eth-phishing-detect/list.txt
- https://raw.githubusercontent.com/hectorm/hmirror/master/data/fademind-add.2o7net/list.txt
- https://raw.githubusercontent.com/hectorm/hmirror/master/data/fademind-add.dead/list.txt
- https://raw.githubusercontent.com/hectorm/hmirror/master/data/fademind-add.risk/list.txt
- https://raw.githubusercontent.com/hectorm/hmirror/master/data/fademind-add.spam/list.txt
- https://raw.githubusercontent.com/hectorm/hmirror/master/data/kadhosts/list.txt
- https://raw.githubusercontent.com/hectorm/hmirror/master/data/malwaredomainlist.com/list.txt
- https://raw.githubusercontent.com/hectorm/hmirror/master/data/malwaredomains.com-immortaldomains/list.txt
- https://raw.githubusercontent.com/hectorm/hmirror/master/data/malwaredomains.com-justdomains/list.txt
- https://raw.githubusercontent.com/hectorm/hmirror/master/data/matomo.org-spammers/list.txt
- https://raw.githubusercontent.com/hectorm/hmirror/master/data/mitchellkrogza-badd-boyz-hosts/list.txt
- https://raw.githubusercontent.com/hectorm/hmirror/master/data/pgl.yoyo.org/list.txt
- https://raw.githubusercontent.com/hectorm/hmirror/master/data/someonewhocares.org/list.txt
- https://raw.githubusercontent.com/hectorm/hmirror/master/data/spam404.com/list.txt
- https://raw.githubusercontent.com/hectorm/hmirror/master/data/stevenblack/list.txt
- https://raw.githubusercontent.com/hectorm/hmirror/master/data/winhelp2002.mvps.org/list.txt
- https://raw.githubusercontent.com/hectorm/hmirror/master/data/zerodot1-coinblockerlists-browser/list.txt
- https://raw.githubusercontent.com/CHEF-KOCH/Audio-fingerprint-pages/master/AudioFp.txt
- https://raw.githubusercontent.com/CHEF-KOCH/Canvas-fingerprinting-pages/master/Canvas.txt
- https://raw.githubusercontent.com/CHEF-KOCH/WebRTC-tracking/master/WebRTC.txt
- https://gitlab.com/quidsup/notrack-blocklists/raw/master/notrack-blocklist.txt
- https://gitlab.com/quidsup/notrack-blocklists/raw/master/notrack-malware.txt
- https://www.stopforumspam.com/downloads/toxic_domains_whole.txt
- https://github.com/kboghdady/youTube_ads_4_pi-hole/blob/master/youtubelist.txt
- https://raw.githubusercontent.com/mkb2091/blockconvert/master/output/domains.txt
- https://dbl.oisd.nl/
- https://phishing.army/download/phishing_army_blocklist_extended.txt
- https://raw.githubusercontent.com/CHEF-KOCH/Audio-fingerprint-pages/master/AudioFp.txt
- https://raw.githubusercontent.com/CHEF-KOCH/Canvas-fingerprinting-pages/master/Canvas.txt
- https://raw.githubusercontent.com/CHEF-KOCH/WebRTC-tracking/master/WebRTC.txt
- https://raw.githubusercontent.com/deathbybandaid/piholeparser/master/Subscribable-Lists/ParsedBlacklists/AakList.txt
- https://raw.githubusercontent.com/deathbybandaid/piholeparser/master/Subscribable-Lists/ParsedBlacklists/Prebake-Obtrusive.txt
- https://jasonhill.co.uk/pfsense/ytadblock.txt
- https://raw.githubusercontent.com/notracking/hosts-blocklists/master/hostnames.txt
- https://raw.githubusercontent.com/StevenBlack/hosts/master/alternates/fakenews-gambling-porn-social/hosts
- https://raw.githubusercontent.com/lightswitch05/hosts/master/ads-and-tracking-extended.txt
- https://raw.githubusercontent.com/lightswitch05/hosts/master/ads-and-tracking.txt
- https://raw.githubusercontent.com/lightswitch05/hosts/master/tracking-aggressive-extended.txt
- https://raw.githubusercontent.com/lightswitch05/hosts/master/tracking-aggressive.txt
- https://hosts-file.net/ad_servers.txt
- https://justdomains.github.io/blocklists/lists/easylist-justdomains.txt
- https://justdomains.github.io/blocklists/lists/easyprivacy-justdomains.txt
- https://justdomains.github.io/blocklists/lists/adguarddns-justdomains.txt
- https://justdomains.github.io/blocklists/lists/nocoin-justdomains.txt
- https://raw.githubusercontent.com/austinheap/sophos-xg-block-lists/master/yoyo-org.txt
- https://raw.githubusercontent.com/austinheap/sophos-xg-block-lists/master/steven-blacks-unified-list.txt
- https://raw.githubusercontent.com/austinheap/sophos-xg-block-lists/master/adguard.txt
- https://raw.githubusercontent.com/austinheap/sophos-xg-block-lists/master/mitchell-krogs-badd-boyz-hosts.txt
- https://raw.githubusercontent.com/austinheap/sophos-xg-block-lists/master/coinblocker.txt
- https://raw.githubusercontent.com/austinheap/sophos-xg-block-lists/master/easylist.txt
- https://raw.githubusercontent.com/austinheap/sophos-xg-block-lists/master/easyprivacy.txt
- https://raw.githubusercontent.com/austinheap/sophos-xg-block-lists/master/kadhosts.txt
- https://raw.githubusercontent.com/austinheap/sophos-xg-block-lists/master/nocoin.txt
- https://raw.githubusercontent.com/austinheap/sophos-xg-block-lists/master/spotifyads.txt
- https://raw.githubusercontent.com/austinheap/sophos-xg-block-lists/master/steven-blacks-ad-hoc-list.txt
- https://raw.githubusercontent.com/austinheap/sophos-xg-block-lists/master/uncheckyads.txt
- https://raw.githubusercontent.com/austinheap/sophos-xg-block-lists/master/adaway.txt
- https://raw.githubusercontent.com/austinheap/sophos-xg-block-lists/master/add-2o7net.txt
- https://raw.githubusercontent.com/austinheap/sophos-xg-block-lists/master/add-dead.txt
- https://raw.githubusercontent.com/austinheap/sophos-xg-block-lists/master/add-risk.txt
- https://raw.githubusercontent.com/austinheap/sophos-xg-block-lists/master/add-spam.txt
- https://raw.githubusercontent.com/austinheap/sophos-xg-block-lists/master/malware-domain-list.txt
- https://raw.githubusercontent.com/austinheap/sophos-xg-block-lists/master/mvps-hosts-file.txt
- https://raw.githubusercontent.com/austinheap/sophos-xg-block-lists/master/dan-pollock-someonewhocares-org.txt
- https://raw.githubusercontent.com/austinheap/sophos-xg-block-lists/master/tyzbit.txt
- https://mirror1.malwaredomains.com/files/justdomains
- https://zeustracker.abuse.ch/blocklist.php?download=domainblocklist
- https://s3.amazonaws.com/lists.disconnect.me/simple_tracking.txt
- https://s3.amazonaws.com/lists.disconnect.me/simple_ad.txt

