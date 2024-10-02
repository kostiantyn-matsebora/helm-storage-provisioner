# Storage provisioner

[![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=kostiantyn-matsebora_helm-storage-provisioner&metric=alert_status)](https://sonarcloud.io/summary/new_code?id=kostiantyn-matsebora_helm-storage-provisioner)

Helm chart for provisioning storage definition (PersistentVolumeClaim and PersistentVolume objects).

Can be useful in the following cases:

* When you want to separate storage and application management.
* When you want to bind `PersistenVolume` with an already existing  volume handle (for instance manually created [Longhorn](https://longhorn.io/) volume.)

## Configuration

```yaml
volumes:
   # Name of PVC and PV
  - name: #  media
    # Size of volume
    size: # 400Gi
  # Name of storage class
    storageClassName: # longhorn-large
    # Name of Longhorn pre-created volume
    volumeHandle: # media-storage
    # List of volume access modes
    accessModes: []
    pv: # Optional, need to specify only if do not want to create pv, by default true
      enabled: # true
    
    pvc: # Optional, need to specify only if do not want to create pv, by default true      
      enabled: # true
```

## Example

```yaml
volumes:
- accessModes:
  - ReadWriteMany
  name: media
  size: 400Gi
  storageClassName: longhorn-large
  volumeHandle: media-storage
- accessModes:
  - ReadWriteMany
  name: qbittorrent-downloads
  size: 10Gi
  storageClassName: longhorn-fast
  volumeHandle: downloads
- accessModes:
  - ReadWriteOnce
  name: jellyfin-cache
  size: 5Gi
  storageClassName: longhorn-fast
  volumeHandle: jellyfin-cache
```

## Usage

Add helm [repository](https://kostiantyn-matsebora.github.io/helm-charts/) first:

```bash
helm repo add kostiantyn-matsebora https://kostiantyn-matsebora.github.io/helm-charts/
```

Install/upgrade helm chart using your custom values:

```bash

# oauth2-proxy
helm upgrade storage kostiantyn-matsebora/storage-provisioner --install --values ./custom-values.yaml

```

## Contributing

If you experience any issues, have a question or a suggestion, or if you wish
to contribute, feel free to [open an issue][issues] or
[start a discussion][discussions].

[issues]: https://github.com/kostiantyn-matsebora/storage-provisioner/issues
[discussions]: https://github.com/storage-provisioner/discussions

## License

[`MIT License`](../LICENSE)
