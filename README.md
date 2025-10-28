# freemyipd

A Linux daemon to maintain dynamic DNS records and SSL/TLS certificates for the [freemyip.com](https://freemyip.com/) service

### Usage:

    [variables] freemyipd [options]

    freemyipd is configured by a combination of environment variables and runtime
    options

    Command options:
      -h, --help           show this message and exit
      -c, --config <path>  source variables from config file
      -4, --ddns-ipv4      maintain DNS A record
      -6, --ddns-ipv6      maintain DNS AAAA record
      -e, --certificate    maintain SSL/TLS wildcard certificate
      -n, --nat            get ipv4 address from the web when behind NAT
          --about          show program description
          --               any arguments after -- will be passed to bash and
                           executed when new certificates are received

    Environment variables:
      TOKEN=     freemyip token. required
      DOMAIN=    freemyip subdomain. required
      DEVICE=    network device to watch. not valid with --nat
      INTERVAL=  polling interval in seconds. defaults to 60, or 600 when behind NAT
      LOGFILE=   log file. leave unset to log to syslog
      EMAIL=     email address to use for Let's Encrypt account
      LEGOPATH=  path to store Let's Encrypt account and certificate. defaults to
                 $HOME/.lego
      CERTUSER=  user who needs read access to the TLS certificate, if different
                 than the calling user
      RENEWBY=   days before certificate expiration to attempt renewal. defaults to
                 15

### Discussion:

The public IP address is polled, using either the local routing table or URL lookup, and is synchronized with [freemyip.com](https://freemyip.com/) when a change is detected. TLS certificates are obtained from [Let's Encrypt](https://letsencrypt.org/) and managed using [lego](https://go-acme.github.io/lego/).
