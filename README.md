# geant-rkpi-invalid



This repo is a simple output of a script that runs at 1900 UTC every evening. It uses code from https://github.com/job/rpki-ov-checker and some other glue to pull routing tables from the GEANT core network, compare against a list of ROA and spits out a list of all the prefixes without a valid ROA, for whom there is no covering ROA (shorter/less specific).

This might be useful if you are a member of GEANT's network and are curious to see which routes are going to be impacted from the 23rd March 2020, when we begin dropping invalid ROA on non-R&E peers.