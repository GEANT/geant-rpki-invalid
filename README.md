# geant-rkpi-invalid

## Introduction
This repo is a simple output of a script that runs at 1900 UTC every evening. It uses code from https://github.com/job/rpki-ov-checker and some other glue to pull routing tables from the GEANT core network, compare against a list of ROA and spits out a list of all the prefixes without a valid ROA, for whom there is no covering ROA (shorter/less specific).

This might be useful if you are a member of GEANT's network and are curious to see which routes are going to be impacted from the 23rd March 2020, when we begin dropping invalid ROA on non-R&E peers. This represents routes that will become unreachable.

## Files
This repo contains 3 files - output from our IPv4 internet routing table, IPv6 routing table - and this Readme.

## Example

An NREN "FOOREN" signs a /16 of IPv4 space, generating a valid ROA. This is advertised and seen by GEANT. They then lend 192.0.2.0/24 to an institute in their country, BAZ. BAZ has their own ASN, and begin to originate 192.0.2.0/24 with their ASN 65535. 

GEANT now sees FOOREN's /16 (valid) and BAZ's /24 (invalid). This is due to no ROA existing for 192.0.2.0/24 with origin ASN 65535. 

The output in this repo would not contain 192.0.2.0/24, as while it is invalid, there is a covering ROA from the parent /16. The /24 would be dropped by GEANT (as we will drop invalid prefixes from March 23, 2020), but traffic will still pass toward FOOREN (and then on to BAZ). This repo contains prefixes (and origin ASN) for invalid ROAs with no covering valid or unknown. These represent networks that will not be reachable from March 23rd, 2020 - at least from the GEANt perspective. 

