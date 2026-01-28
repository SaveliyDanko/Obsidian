#linux #filesystem 

---
**Formatting** means creating a filesystem inside a volume so that Linux can store and retrieve files from it.

Example:
```bash
sudo mkfs.ext4 /dev/sdb1
```

This command:
- Initializes the `/dev/sdb1` partition with the ext4 filesystem,
- Creates internal structures (e.g. superblocks, inodes, directory trees).

You can also use other filesystems like `xfs`, `btrfs`, `vfat`, etc.
