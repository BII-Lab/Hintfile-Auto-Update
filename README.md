#HintfileAutoUpdate

Introduction
------------
With the nearest renumbering plan of H root Server's IP address, there is a discussion of ways resolvers 
updating their hintfile. Traditional ways includes using ftp protocol by doing a wget and dig servers' address manually.
Each way would depend on operators manual operation. As a result, there is many old machines could not update its hint-file
rightly. As a proof, after done renumbering for thirteen years, there is an observation that the "Old J-Root" can still
receives DNS query traffic.

This project aims to find a automatic way for hint-file updating. The already-done works is a shell script which provides
the function that update a hint-file in file system automatically with DNSSEC and trust anchor validation

Construction
------------
It is a shell script so it does not require any compile or installation. Just put script into the operation system and giant
it excute accession. Until now, the script depends on dig command. The future would make the script compatible with PowerDNS
user and drill command.

Methodology and Usage
------------
The script will query the NS list for "." domain and query A and AAAA record for every domain on the NS list. it will also
validation DNSSEC and trust anchor for all the answer. You can specify the path for root key by the option --fetchkeys or
the script will query the root key itself and delete it after runnling. After getting all the answers, the script will 
compare the new hintfile to the old one. If there is a difference, it will rename the old one with a timestamp and replace 
the old one with the new one. Otherwise the script will delete the new hintfile and nothing will be changed.

Start the script like:
	./hintUpdateScript $hint-file-path (--fetchkeys rootkey path)
the parameters in parentheses are optional.