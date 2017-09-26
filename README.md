# cheeese

*A ZFS snapshotter for intermittently-powered systems.*

### Why does this exist? Aren't there enough snapshot tools already?

Probably. Most of them likely better than this one.

### So, why?

I don't keep all my computers turned on all the time.

### But, wh... wait, what?

Most existing snapshot tools store snapshot life metadata, either in the snapshot name or elsewhere.

Cheeese does not.

So, for example, a snapshot that was a result of a 'daily' rule but is the only one that exists for a particular week, will be retained as a weekly copy.

This makes Cheeese more suitable for systems that aren't running 24/7.

## Usage

Cheeese has no configuration and gets its schedule from command-line arguments.

A sample routine could look like the following:

```cheeese 30m3 h2 d5 w3 m5 y0 --cleanup=2d```

Run every 30 minutes (eg. via `cron`), this would translate to:

Keep...

- **3** 30-minute-ly snapshots
- **2** hourly snapshots\*
- **5** daily snapshots
- **3** weekly snapshots
- **5** monthly snapshots
- **unlimited** yearly snapshots
- And clean up (remove unwanted snapshots) every 2 days.

\* The `h2` is actually redundant here, as Cheeese's design means statements are deduplicated. Ergo, a definition for 3 30-minutely snapshots already covers 2 hourly snapshots (but no more).

Cheeese calculates time periods by counting backwards from the time of its initialization.

## Disclaimer

This is a utility whose purpose is to delete things. It may, therefore, delete things.

I am not responsible if it goes wrong and deletes more than it's supposed to, agitates your cat, or (God forbid) converts your filesystem to BTRFS.

If you're not comfortable with this, you should turn around now.
