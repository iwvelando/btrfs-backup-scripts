# btrfs-backup-scripts

This is a collection of scripts intended to aid in creating a varied set of read-only btrfs subvolume snapshots.

# Requirements

Most fundamentally, you need a [btrfs filesystem](https://btrfs.wiki.kernel.org/index.php/Main_Page) with the btrfs administration tools installed; Arch Linux users can run

    pacman -S btrfs-progs

to install them.

# Configuration

There are four scripts included:

* *btrfs-snap-daily, btrfs-snap-weekly, btrfs-snap-monthly*: designed to create snapshots of every subvolume on a daily, weekly, or monthly basis respectively
* *btrfs-snap-stable*: designed to create snapshots of every subvolume on a manual basis when the user feels the system is at a stable point

These scripts are currently heavily tailored to my specific btrfs setup which was created according to [this guide](http://wongdev.com/blog/pure-btrfs-installation/) by Andrew Wong; the scripts on the whole will need to be customized for an individual's needs, but the basic concept can be adapted. Each script is set up analogously but is meant to end up in a different area of the system and should have independent configurations, hence the separation. The configurables are located at the top of each file:

* *maxSets*: how many sets of snapshots generated by this script to keep
* *subvolsPerSet*: hard code how many subvolumes each set of snapshots will contain (not variable)
* *subvolDir*: root directory of snapshots
* *subvolActiveDir*: directory where actively mounted subvolumes are stored
* *subvolSnapshotDir*: directory where snapshots are stored
* *prefix*: prefix for this script's snapshots

# Implementation

Once the scripts are configured and tailored to your btrfs setup, the intended use is to place the daily, weekly, and monthly scripts in
    /etc/cron.{daily,weekly,monthly}
respectively. The stable script should be placed in root's $PATH or symlinked there.

Once placed the idea is to let the periodic snapshots run their course and to run the stable snapshot when you feel your system is at a stable milestone or before a potentially risky action; this variety of snapshots should provide a strong safeguard against errors.

# Next Steps

## Create a restoration script
## Come up with smarter ways of detecting a system's configuration to reduce hard-coding
