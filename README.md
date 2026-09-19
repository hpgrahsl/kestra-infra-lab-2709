# Training namespace files

This repository stores the Namespace Files used by the Kestra infra management training lab.

## Layout

```text
linux/
  ansible_write_marker/
windows/
  winrm_download_probe/
  winrm_read_check/
  winrm_write_marker/
```

Each directory contains the Ansible inventory and playbook consumed by the correspondingly named training flow. Paths are preserved when Kestra imports the files; for example, `linux/ansible_write_marker/site.yml` is written to the Linux child namespace as `ansible_write_marker/site.yml`.

## Synchronization

Each participant namespace receives a disabled `sync_namespace_files` flow. Once enabled, it pulls `linux/` into `training.participantNN.linux` and `windows/` into `training.participantNN.windows` using `io.kestra.plugin.git.SyncNamespaceFiles`.

Configure the repository URL and branch through `LAB_GIT_REPOSITORY_URL` and `LAB_GIT_BRANCH` in the lab bootstrap configuration. The repository may be public; no Git credential is required for public HTTPS cloning.

The corresponding sync flow on Kestra side currently uses `delete: false`, so removing a file from this repository does not remove its existing Kestra Namespace File.
