A role to read certificates from Vault and install them on remote hosts for use
by local services. `ssl_cert_dir` defaults to `/etc/letsencrypt` and can be overridden.

Installed certificates and private keys use mode 0644 (world-readable). This is an
explicitly accepted risk: several local agents/services running as different
users consume the shared wildcard key, and tighter permissions would break those
consumers. Any local user can read the private key. This does not make the key
non-secret or safe to expose beyond those hosts.

`install_certs_remote.yml` inherits the caller's privilege settings for endpoint
writes. Administrative installers connecting as an administrator should set
`become: true` and `become_user: "{{ cert_owner }}"` on the role import. Renewal
jobs can connect directly as `cert_owner` (default `certpush`) without become;
the account itself does not need sudo. Vault reads remain delegated to the
controller with `become: false`, regardless of the caller's become keywords.
