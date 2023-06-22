Linode module for Caddy
=======================

This package contains a DNS provider module for [Caddy](https://github.com/caddyserver/caddy). It can be used to manage DNS records with Linode.

## Caddy module name

```
dns.providers.linode
```

## Building

To compile this Caddy module, follow the steps describe at the [Caddy Build from Source](https://github.com/caddyserver/caddy#build-from-source) instructions and import the `github.com/caddy-dns/linode` plugin

## Authenticating

See [the associated README in the libdns package](https://github.com/libdns/linode) for important information about credentials.

## Config examples

To use this module for the ACME DNS challenge, [configure the ACME issuer in your Caddy JSON](https://caddyserver.com/docs/json/apps/tls/automation/policies/issuer/acme/) like so:

```json
{
	"module": "acme",
	"challenges": {
		"dns": {
			"provider": {
				"name": "linode",
				"api_token": "{env.LINODE_PERSONAL_ACCESS_TOKEN}",
				"api_url": "{env.LINODE_API_URL}",
				"api_version": "{env.LINODE_API_VERSION}"
			}
		}
	}
}
```

or with the Caddyfile:

```
# globally
{
	acme_dns linode {env.LINODE_PERSONAL_ACCESS_TOKEN}
}

# globally, with optional fields
{
	acme_dns linode {
	  api_token {env.LINODE_PERSONAL_ACCESS_TOKEN}
	  api_url {env.LINODE_API_URL}
	  api_version {env.LINODE_API_VERSION}
	}
}
```

```
# one site
tls {
	dns linode {$LINODE_PERSONAL_ACCESS_TOKEN}
}

# one site, with optional fields
tls {
	dns linode {
	  api_token {$LINODE_PERSONAL_ACCESS_TOKEN}
	  api_url {env.LINODE_API_URL}
	  api_version {env.LINODE_API_VERSION}
	}
}
```

You can replace `{$*}` or `{env.*}` with the actual values if you prefer to put it directly in your config instead of an environment variable.

The fields are:

- `api_token` - The Linode Personal Access Token to use.

- `api_url` - The Linode API hostname to use, i.e. `api.linode.com`.

- `api_version` - The Linode API version to use, i.e. `v4`.
