# SpawnpointClusterTool
This tool is used to take a list of coordinates (spawnpoints, gyms, pokestops) and output the center location that covers a configurable amount of points. The output will also be sorted using the TSP formula. This project is written in Python and based on the spawnpoint functionality used in the RocketMap spawnpoint routing functions.

# Get Started With Python
This script was written with Python3.6.

To get started using the python script, you can download the files or `git clone https://github.com/Kneckter/SpawnpointClusterTool` this repository.

You will need a few Python3 modules to run this script so run this command: `sudo -H pip3 install -U configargparse==0.14.0 peewee==3.9.6 matplotlib==3.1.1 PyMySQL==0.9.3 geopy==1.20.0`

You do not need to create lists of coordinate pairs, this tool has settings to connect to your database and read a geofence that is part of a questing instance. 
Make a copy of the `config.ini.example` and rename it as `config.ini`. Fill in the database settings for your RDM database.

Review the other options in the config file. All options in the config file can be passed on the command line, which can be viewed with the `-h` or `--help` flags.

- '--db-name', Name of the database to be used (required).
- '--db-user', Username for the database (required).
- '--db-pass', Password for the database (required).
- '--db-host', IP or hostname for the database (defaults to 127.0.0.1).
- '--db-port', Port for the database (defaults to 3306).

- '-cf', '--config', Set configuration file (defaults to ./config.ini).')
- '-geo', '--geofence', The name of the RDM quest instance to use as a geofence (required).
- '-of', '--output', The base filename without extension to write cluster data to (defaults to outfile).
- '-ns', '--nosort', Do not sort the output from the search (defaults to false).

- '-sp', '--spawnpoints', Have spawnpoints included in cluster search (defaults to false).
- '-r', '--radius', Maximum radius (in meters) where spawnpoints are considered close (defaults to 70).
- '-ms', '--min', The minimum amount of spawnpoints to include in clusters that are written out (defaults to 3).
- '-ct', '--timers', Choose whether to use confirmed spawn timers (yes), use unconfirmed timers (no), or all timers (all) (defaults to all).
- '-lu', '--lastupdated', Only use spawnpoints that were last updated in x hours. Use 0 to disable this option (defaults to 0).

- '-ps', '--pokestops', Have pokestops included in the cluster search (defaults to false).
- '-gym', '--gyms', Have gyms included in the cluster search (defaults to false).
- '-mr', '--minraid', The minimum amount of gyms or pokestops to include in clusters that are written out (defaults to 1).
- '-rr', '--raidradius', Maximum radius (in meters) where gyms or pokestops are considered close (defaults to 500).

- '-giv', '--genivlist', Skip all the normal functionality and just generate an IV list using RDM data (defaults to false).
- '-mp', '--maxpoke', The maximum number to be used for the end of the IV list (defaults to 809).
- '--excludepoke', List of Pokemon to exclude from the IV list. Specified as Pokemon ID. Use this only in the config file (defaults to none).

- '-cc', '--circle', Create circles from a geofence instance. Requires -geo <name> and -r <#>. Sorting should be disabled (defaults to false).

You must specify an instance to use in the `geofence` parameter so the script can search for it. Instances with multiple geofences are acceptable. The script will read and apply each geofence to the query.

If searching for clusters, you must choose to include either spawnpoints, gyms, or pokestops for the query.

Once you have the config file on your system you can run the command `python3 cluster.py` to to have it evaluate the coordinates, sort them by TSP, and output them to outfile file.

## Notes
This has been tested on Ubuntu 18.04. 
