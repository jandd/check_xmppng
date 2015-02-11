# check_xmppng - check plugin for XMPP

This program implements a nagios check plugin for XMPP servers implementing the
XMPP protocol as specified in [RFC 6120](http://tools.ietf.org/html/rfc6120).

The program implements the following features:

* check client to server (C2S) as well as server to server (S2S) ports
* check XMPP servers on IPv6 and IPv4 addresses
* support STARTTLS as specified in RFC 6120 section 5.
* check the validity of the server certificate presented by the XMPP server

The plugin has been implemented because of insufficiencies in check_ssl_cert
and the existing [check_xmpp](https://exchange.icinga.org/exchange/check_xmpp).

Maximum acceptable timeouts as well as minimum acceptable number of days the
server certificate needs to be valid can be specified as command line
parameters. For a full list of parameters see the *Usage* section below.


## Dependencies

The program is implemented in Python 3 and uses the following libraries besides
the Python standard library:

* [defusedxml](https://pypi.python.org/pypi/defusedxml/) to sanitize XML from
  the XMPP server
* [nagiosplugin](https://pypi.python.org/pypi/nagiosplugin) to take care of the
  nagios plugin interface boilerplate code

The software has been developed and tested with the following versions:

* Python 3.4.2
* defusedxml 0.4.1
* nagiosplugin 1.2.2


## License

check_xmppng is free software: you can redistribute it and/or modify it under
the terms of the GNU General Public License as published by the Free Software
Foundation, either version 3 of the License, or (at your option) any later
version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY
WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A
PARTICULAR PURPOSE.  See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with
this program in the file `COPYING`.  If not, see
http://www.gnu.org/licenses/.


## Usage

```
usage: check_xmpp [-h] -H HOST_ADDRESS [-p PORT] [--s2s | --c2s] [-4 | -6]
                  [--servername SERVERNAME] [--starttls] [-w SECONDS]
                  [-c SECONDS] [--no-check-certificates] [-r CAROOTS]
                  [--warn-days WARNDAYS] [--crit-days CRITDAYS] [-v]

Check XMPP services

optional arguments:
  -h, --help            show this help message and exit
  -H HOST_ADDRESS, --host-address HOST_ADDRESS
                        host address
  -p PORT, --port PORT  port
  --s2s                 server to server (s2s)
  --c2s                 client to server (c2s)
  -4, --ipv4            enforce IPv4
  -6, --ipv6            enforce IPv6
  --servername SERVERNAME
                        server name to be used
  --starttls            check whether the service allows starttls
  -w SECONDS, --warning SECONDS
                        return warning if connection setup takes longer than
                        SECONDS
  -c SECONDS, --critical SECONDS
                        return critical if connection setup takes longer than
                        SECONDS
  --no-check-certificates
                        do not check whether the XMPP server's certificate is
                        valid
  -r CAROOTS, --ca-roots CAROOTS
                        path to a file or directory where CA certifcates can
                        be found
  --warn-days WARNDAYS  set state to WARN if the certificate is valid for not
                        more than the given number of days
  --crit-days CRITDAYS  set state to CRITICAL if the certificate is valid for
                        not more than the given number of days
  -v, --verbose
```


## Contact

If you want to provide feedback or bug reports please send me a mail to
jan (at) dittberner [dot] info.
