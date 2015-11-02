# exabgp-prefix-file

Manage a list of prefixes in a file and have them announced to or withdrawn from ExaBGP automatically. This is useful for instance to have certain addresses blackholed automatically when they are added to a file.

## daemon

This should be run as a `process' in ExaBGP. Use an ExaBGP configuration similar to:

<pre>
neighbor 127.0.0.1 {
    router-id 192.0.2.1;
    local-address 127.0.0.1;
    local-as 64520;
    peer-as 64519;
    graceful-restart;

    process blackhole {
        run /path/to/daemon --prefix-file=/path/to/prefixes --community=64519:666;
    }
}
</pre>

The options for the daemon are as follows:

<pre>
usage: daemon [-h] --prefix-file PATH [--community COMMUNITY] [--next-hop IP]
              [--interval SECONDS]

Monitor a file for additions and removals of IP addresses. Output these
changes to stdout in a format suitable for ExaBGP. Michael Fincham
<michael.fincham@catalyst.net.nz>

optional arguments:
  -h, --help            show this help message and exit
  --prefix-file PATH    path to prefix list that will be monitored
  --community COMMUNITY
                        community to be attached to announced prefixes,
                        defaults to no community
  --next-hop IP         next-hop to be attached to announced prefixes,
                        defaults to 192.0.2.1
  --interval SECONDS    polling interval in seconds, defaults to 5
</pre>
