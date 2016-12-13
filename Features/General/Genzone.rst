


Zone file generation
--------------------

FRED can be used to automate the zone-file generation process.

It is possible to manage multiple different (even overlapping) zones.
For each zone, the generator will create zone files with SOA, NS, A, AAAA,
and DS records as specified in the Registry database.

The zone-file generation process is protected by configurable change counters
– if the number of changes is too high, the process is blocked until manual
resolution.
