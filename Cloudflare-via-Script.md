Script will: (1) add (or update) all the Cloudbox [[subdomains|Basics: Accessing Cloudbox Apps#default apps]] into Cloudflare, and (2) will enable DNS and HTTP proxy (CDN) for Plex.

Steps to setup Cloudflare are as follows:

1. Sign up for a free [Cloudflare](https://www.cloudflare.com/) account.

1. Set the Name Servers to what Cloudflare instructs you to on your Domain Registrar's website (e.g. GoDaddy, Namecheap, etc). _You do not need to make changes to the DNS settings there._

   - Ex. Namecheap.com -> "Dashboard" -> your domain -> "Manage" -> "Name Servers" -> "Custom DNS" -> add the nameservers in.

     ![](https://i.imgur.com/K4OI1XD.png)

1. Go to [Cloudflare.com](https://www.cloudflare.com/).

   1. Under the "Crypto" tab, set "SSL" to `Full (strict)`.

      ![](https://i.imgur.com/ph1pNZx.png)

   1. Under the "Overview" tab, click "Get your API key", then retrieve your "Global API Key".

      ![](https://i.imgur.com/9ANNz68.png)

1. Run the following python script:

   ```
   python3 /opt/scripts/cloudflare/cloudflared.py
   ```

1. When asked, enter your email address, API key, domain, and server IP address.

   _Note 1: The script will only set the subdomains to one IP address. If you have a separate Plex and Feeder setup, you will need to login to Cloudflare and adjust the IP addresses for their respective subdomains._


   _Note 2: From now on, any DNS settings changes and/or adding of subdomains will now be done on Cloudflare instead of your Domain Registrar's website._

