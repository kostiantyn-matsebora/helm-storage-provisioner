# Storage provisioner

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
