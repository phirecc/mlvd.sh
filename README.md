# mlvd
A small (under 100 LOC) POSIX shell script that lets you connect to Mullvad servers through
Wireguard. No background services, no extras, easily auditable.

## Installation
Dependencies: 

- jq
- curl
- wg-quick (wireguard-tools)
- openresolv (for dns)

To install them on arch:
```
sudo pacman -S --needed jq curl wireguard-tools openresolv
```

You can install `mlvd` manually like so:
```
git clone https://github.com/phirecc/mlvd
cd mlvd
sudo install -Dm600 template.conf /var/lib/mlvd/template.conf
sudo install -Dm755 mlvd /usr/bin/mlvd
```

Or through an AUR package:
```
paru -S mlvd
```

## Configuration
To configure your user account, download a wireguard config from [your account
panel](https://mullvad.net/en/account/#/wireguard-config/) and copy its `PrivateKey` and `Address`
values into `/var/lib/mlvd/template.conf`

`mlvd` will replace the `SERVER_IP` and `SERVER_PUBKEY` placeholders with the respective values for
the server you want to connect to. Other than that the template can be modified like any other
Wireguard config.

Once that's done you should be able to connect to a server:
```
sudo mlvd c de
```

To get a list of available servers run:
```
mlvd l
```

The connect method looks for prefixes of server hostnames, so to connect to a specific city you
could do:
```
sudo mlvd c de-fra
```

Or to connect to a specific server:
```
sudo mlvd c de-fra-wg-402
```

## Note
This third-party project is in no way affiliated with Mullvad.
