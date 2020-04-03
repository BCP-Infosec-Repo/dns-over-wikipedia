# DNS over Wikipedia

Wikipedia keeps track of official URLs for popular websites. DNS over Wikipedia locally resolves domains ending with `.idk` using the URL listed on a topic's Wikipedia page. 

> Instead of googling for the site, I google for the site's Wikipedia article ("schihub wiki") which usually has an up-to-date link to the site in the sidebar, whereas Google is forced to censor their results.  
> If you Google "Piratebay", the first search result is a fake "thepirate-bay.org" (with a dash) but the Wikipedia article lists the right one.
> — [shpx](https://news.ycombinator.com/item?id=22414031)

## Installation Instructions
Required dependencies:

 - dnsmasq
   - Ubuntu: `sudo apt install dnsmasq`
   - macOS: `brew install dnsmasq`
 - Rust (and Cargo)

### 1. Configure dnsmasq
#### Linux:
Add the following to your `dnsmasq.conf`:
```
address=/idk/127.0.0.1
```

#### macOS:
```bash
echo "address=/.idk/127.0.0.1" >> "$(brew --prefix)/etc/dnsmasq.conf"
sudo brew services start dnsmasq
```

### 2. Use dnsmasq to resolve queries
#### Linux:
I believe the typical installation on linux handles this.

#### macOS:
```bash
sudo mkdir -p /etc/resolver
sudo tee -a /etc/resolver/idk > /dev/null << EOF
nameserver 127.0.0.1
EOF
```

### 3. Installing

```bash
cargo install --path .
```

### 4. Running
```bash
sudo dns-over-wikipedia
```

Now
