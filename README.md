# Cloudflare DNS Updater

## Overview

**Cloudflare DNS Updater** is a Python script that automatically updates your
Cloudflare **A records** whenever your server’s public IP changes.

The script uses **Cloudflare itself** to detect the current public IP, instead
of relying on third-party services. This approach offers key advantages:

- **High availability:** as long as Cloudflare is up, the script can fetch your
  IP and update the DNS records. If Cloudflare is down, updates wouldn’t work
  anyway.
- **Better reliability:** because it queries Cloudflare by IP instead of
  resolving a hostname, it still works even if DNS resolution fails
  temporarily.

---

## Usage

You’ll need a **Cloudflare API Token** with permission to edit DNS records. If
you don't have one yet, see the section
[Creating a Cloudflare API Token](#creating-a-cloudflare-api-token)
for setup instructions.

Once your token is ready, export it as an environment variable:

```bash
export CLOUDFLARE_API_TOKEN="your_token_here"
```

Then, you can run a one-time update:

```bash
./cloudflare-update-dns
```

Or keep it running every N minutes:

```bash
./cloudflare-update-dns --every 5
```

you can also provide specific subdomains to update:

```bash
./cloudflare-update-dns --subdomains mydomain.com,*.midomain.com
```

Use `--help` to see a full list of available parameters.

---

## Creating a Cloudflare API Token

1. Go to https://dash.cloudflare.com/profile/api-tokens
1. Create a new **API Token** using the **Edit zone DNS** template. This
   template already provides the necessary permissions.
1. (Optional) Restrict the token to specific zones (domains) you want to
   update.
1. Save the token.

---

## License

This project is distributed under the terms of the **MIT License**. See the
[LICENSE](./LICENSE) file for details.
