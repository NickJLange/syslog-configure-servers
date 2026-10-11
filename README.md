A role to read in certs from a vault and write them to a file on the remote host in  /etc/pki/tls/certs/, which is read by other roles as part of service configuration.

Installed certs and keys are written with mode 0644 (world-readable) intentionally. These are wildcard keys shared across many system agents/services on the host, not per-service secrets, so there's no secrecy boundary to enforce with tighter permissions; restricting the mode would just break the other agents that read it.
