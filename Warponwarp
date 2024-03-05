{
  "log": {
    "level": "warn",
    "output": "box.log",
    "timestamp": true
  },
  "dns": {
    "servers": [
      {
        "tag": "dns-remote",
        "address": "udp://1.1.1.1",
        "address_resolver": "dns-direct"
      },
      {
        "tag": "dns-trick-direct",
        "address": "https://sky.rethinkdns.com/",
        "detour": "direct-fragment"
      },
      {
        "tag": "dns-direct",
        "address": "1.1.1.1",
        "address_resolver": "dns-local",
        "detour": "direct"
      },
      {
        "tag": "dns-local",
        "address": "local",
        "detour": "direct"
      },
      {
        "tag": "dns-block",
        "address": "rcode://success"
      }
    ],
    "rules": [
      {
        "domain_suffix": ".ir",
        "geosite": "ir",
        "server": "dns-direct"
      },
      {
        "domain": "cp.cloudflare.com",
        "server": "dns-remote",
        "rewrite_ttl": 3000
      }
    ],
    "final": "dns-remote",
    "static_ips": {
      "sky.rethinkdns.com": [
        "188.114.97.3",
        "188.114.96.3",
        "2a06:98c1:3121::3",
        "2a06:98c1:3120::3",
        "104.18.203.232",
        "104.18.202.232",
        "188.114.96.3",
        "188.114.97.3",
        "2a06:98c1:3121::3",
        "2a06:98c1:3120::3"
      ]
    },
    "independent_cache": true
  },
  "inbounds": [
    {
      "type": "tun",
      "tag": "tun-in",
      "mtu": 9000,
      "inet4_address": "172.19.0.1/28",
      "auto_route": true,
      "strict_route": true,
      "endpoint_independent_nat": true,
      "sniff": true,
      "sniff_override_destination": true
    },
    {
      "type": "mixed",
      "tag": "mixed-in",
      "listen": "127.0.0.1",
      "listen_port": 2334,
      "sniff": true,
      "sniff_override_destination": true
    },
    {
      "type": "direct",
      "tag": "dns-in",
      "listen": "127.0.0.1",
      "listen_port": 6450,
      "override_address": "1.1.1.1",
      "override_port": 53
    }
  ],
  "outbounds": [
    {
      "type": "selector",
      "tag": "select",
      "outbounds": [
        "auto",
        "WarpInWarp✅ § 0",
        "Warp 🇮🇷 IP § 1"
      ],
      "default": "auto"
    },
    {
      "type": "urltest",
      "tag": "auto",
      "outbounds": [
        "WarpInWarp✅ § 0",
        "Warp 🇮🇷 IP § 1"
      ],
      "url": "http://cp.cloudflare.com/",
      "interval": "10m0s"
    },
    {
      "type": "wireguard",
      "tag": "WarpInWarp✅ § 0",
      "local_address": [
        "172.16.0.2/24",
        "2606:4700:110:83cb:231a:9182:4aa7:c4da/128"
      ],
      "private_key": "mIleQ9Ps/vuE374VcLzoomSCm0dHWwO2ap2Jk9k55nc=",
      "server": "188.114.96.118",
      "server_port": 7103,
      "peer_public_key": "bmXOC+F1FxEMF9dyiK2H5/1SUtzH0JuVo51h2wPfgyo=",
      "reserved": "AAAA",
      "mtu": 1280,
      "fake_packets": "8-15",
      "fake_packets_size": "40-100",
      "fake_packets_delay": "20-250"
    },
    {
      "type": "wireguard",
      "tag": "Warp 🇮🇷 IP § 1",
      "detour": "WarpInWarp✅ § 0",
      "local_address": [
        "172.16.0.2/24",
        "2606:4700:110:86fe:cf22:a418:83fe:2b13/128"
      ],
      "private_key": "+CmNoEsUsqTAHuMAQ36ODdquhniW0UplxgZtKNuLZ2U=",
      "server": "188.114.99.120",
      "server_port": 2408,
      "peer_public_key": "bmXOC+F1FxEMF9dyiK2H5/1SUtzH0JuVo51h2wPfgyo=",
      "reserved": "AAAA",
      "mtu": 1120,
      "fake_packets_size": "40-100",
      "fake_packets_delay": "20-250"
    },
    {
      "type": "dns",
      "tag": "dns-out"
    },
    {
      "type": "direct",
      "tag": "direct"
    },
    {
      "type": "direct",
      "tag": "direct-fragment",
      "tls_fragment": {
        "enabled": true,
        "size": "1-500",
        "sleep": "0-500"
      }
    },
    {
      "type": "direct",
      "tag": "bypass"
    },
    {
      "type": "block",
      "tag": "block"
    }
  ],
  "route": {
    "geoip": {
      "path": "geo-assets/sagernet-sing-geoip-geoip.db"
    },
    "geosite": {
      "path": "geo-assets/sagernet-sing-geosite-geosite.db"
    },
    "rules": [
      {
        "inbound": "dns-in",
        "outbound": "dns-out"
      },
      {
        "port": 53,
        "outbound": "dns-out"
      },
      {
        "clash_mode": "Direct",
        "outbound": "direct"
      },
      {
        "clash_mode": "Global",
        "outbound": "select"
      },
      {
        "domain_suffix": ".ir",
        "geosite": "ir",
        "geoip": "ir",
        "outbound": "bypass"
      }
    ],
    "final": "select",
    "auto_detect_interface": true,
    "override_android_vpn": true
  },
  "experimental": {
    "cache_file": {
      "enabled": true,
      "path": "clash.db"
    },
    "clash_api": {
      "external_controller": "127.0.0.1:6756"
    }
  }
}
