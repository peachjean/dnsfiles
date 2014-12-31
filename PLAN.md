I want two commands:
 1. init -- initializes the current directory with your existing gandi config
 2. sync -- updates your gandi config with the current directory info

Directory structure:

domains.yml -- basically domain -> zone file mapping
zones/ -- directory of zone files
zones/my_zone.yml -- a list of records for the given zone, each record includes "type", "name", "ttl", and "value"

The basic sync process:
  for each zone in zones/ dir:
   find zone in api (match by name)
   if zone does not exist:
    create zone (version 1 will exist, it will be empty)
   get the active version.
   validate the latest version -- if it does not match the active version, throw an error
   compare the active version to the zone file
    if different (else continue with next zone):
      create new version
      delete any records that no longer exist
      create new records
      set zone to use new version
  for each domain in domains.yml:
   set domain to use specified zone
