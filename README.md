# Multi-Remote Cloud Storage Experiment (rclone)

A personal configuration experiment using **rclone** to combine multiple Google Drive remote definitions into a single Union remote, with a Chunker remote layered on top.

> **Security note:** This repository intentionally contains no OAuth access tokens, refresh tokens, client secrets, or live account credentials. The example configuration is a topology reference, not a ready-to-use authenticated configuration.

## Architecture

```text
Google Drive remotes (gdrive1 ... gdrive19)
                  |
                  v
        MegaDrive (rclone Union)
                  |
                  v
      MegaDriveChunked (Chunker)
```

## What this configuration demonstrates

- 19 separately named Google Drive remote definitions (`gdrive1` through `gdrive19`).
- An rclone **Union** remote named `MegaDrive` that references those remotes.
- A **Chunker** remote named `MegaDriveChunked` that points to `MegaDrive`.
- Union policy settings recorded in the local configuration: `action_policy = epall`, `search_policy = ff`, `create_policy = mfs`, and `cache_time = 600`.

This README describes the configuration structure only. It does not claim that a public endpoint, continuously available server, or live demo is currently running.

## Files

- `rclone.example.conf` — sanitised example of the remote topology. It contains no authentication tokens or OAuth client credentials.
- `.gitignore` — helps prevent accidentally adding local config files and environment secrets.

## Using this as a reference

1. Install rclone on your own machine.
2. Create and authenticate your Drive remotes locally using `rclone config`.
3. Recreate the Union and Chunker remotes using the example as a structural reference.
4. Keep the real `rclone.conf` in your local rclone configuration directory. Do not commit it, email it, or include it in screenshots.

The example omits authentication fields by design; it is not intended to be copied over a working local configuration.

## Security

- Never commit `rclone.conf`, OAuth tokens, refresh tokens, client secrets, `.env` files, or passwords.
- Do not publish an encrypted real config as a substitute for redaction. Keep the real config private.
- If credentials are ever exposed, revoke/rotate them at the provider before cleaning repository history. Removing a secret in a later commit does not remove it from earlier Git history.
