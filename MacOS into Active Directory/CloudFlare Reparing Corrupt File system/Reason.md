Cloudflare sever hosted on proxmox crashed and stopped working for some reason, starting it produced a error : -
Trying to start it again in a debug mode still produces a failed error
```
pct start 100 --debug
```

![[Pasted image 20260207112127.png]]

#### What could be the reason: -

**broken or unreadable container root filesystem**

###### What the error is really saying

The key line is this:

`can't read superblock on /dev/mapper/pve-vm--100--disk--0`

That means:
- Proxmox tried to mount the container’s disk.
- The Linux kernel could **not read the filesystem metadata (superblock)**
- So the container never even gets to start

In short: **the container disk is damaged or not a valid filesystem anymore**.

---

##### Most common causes (ranked)

###### 1️⃣ Filesystem corruption (most likely)

Usually caused by:

- Host crash / power loss
- Storage hiccup
- Forced reboot while the container was writing

This is _very_ common with LXC containers.

---

###### 2️⃣ Wrong filesystem type

If the disk was created as `xfs` but Proxmox expects `ext4` (or vice versa), mounting fails with the same error.

---

###### 3️⃣ Broken LVM / storage backend

Less common, but possible if:
- The logical volume exists but is partially corrupted
- Underlying disk has errors

---









#### Action
##### First thing to check (safe & fast)

###### Verify the disk exists

`ls -l /dev/mapper/pve-vm--100--disk--0`

If it’s missing → storage problem  
If it exists → filesystem problem (most likely)

---

###### Check what filesystem it _should_ be

`blkid /dev/mapper/pve-vm--100--disk--0`

You’ll usually see something like:

`TYPE="ext4"`

If nothing shows up → superblock is damaged.

---

###### Try repairing the filesystem (⚠️ important)

### If it’s **ext4** (most common)

`pct stop 100 fsck.ext4 -f /dev/mapper/pve-vm--100--disk--0`

Answer **`y`** to fixes.

👉 This fixes the problem **a huge percentage of the time**.

---

### If it’s **xfs**

`xfs_repair /dev/mapper/pve-vm--100--disk--0`

---

## After repair

`pct start 100`

If it starts → you’re done 🎉  
If not → grab the _first new error_, not the old one.