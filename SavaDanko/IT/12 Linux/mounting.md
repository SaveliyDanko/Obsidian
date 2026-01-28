#linux #filesystem 

---
In Linux, the entire system is a single directory tree rooted at `/`.  
**Mounting** means attaching a volume to a specific directory so that its files become accessible.

Example:
```bash
sudo mount /dev/sdb1 /mnt/data
```

This makes the contents of `/dev/sdb1` available under `/mnt/data`.

After mounting, you can `cd /mnt/data` and work with files stored on that volume.
