# Network File System (NFS)

Network File System (NFS) is a distributed file system protocol that allows a user on a client computer to access files over a network as if they were on the local storage.

## Features
- **File Sharing**: Enables multiple clients to access shared files.
- **Scalability**: Supports a large number of clients in a distributed environment.
- **Authentication & Security**: Uses authentication methods like Kerberos.
- **Performance**: Supports caching to improve read performance.
- **Cross-Platform**: Available on Linux, Unix, and Windows.

## NFS Components
1. **NFS Server**: Hosts shared directories and provides access to clients.
2. **NFS Client**: Accesses the shared directories on the NFS server.
3. **Mount Points**: Locations where the NFS shares are mounted on the client system.
4. **Exports File**: `/etc/exports` defines shared directories and client permissions.

## NFS Versions
- **NFSv2**: Older version with limited features.
- **NFSv3**: Supports larger file sizes, better performance, and asynchronous writes.
- **NFSv4**: Introduces stateful operations, ACLs, and better security.

## How to Set Up NFS
### On the Server:
1. Install the NFS server:
   ```sh
   sudo apt update && sudo apt install nfs-kernel-server -y
   ```
2. Create a shared directory:
   ```sh
   sudo mkdir -p /mnt/shared
   sudo chown nobody:nogroup /mnt/shared
   ```
3. Configure `/etc/exports`:
   ```sh
   /mnt/shared 192.168.1.0/24(rw,sync,no_subtree_check)
   ```
4. Apply the changes:
   ```sh
   sudo exportfs -a
   sudo systemctl restart nfs-kernel-server
   ```

### On the Client:
1. Install the NFS client:
   ```sh
   sudo apt update && sudo apt install nfs-common -y
   ```
2. Mount the NFS share:
   ```sh
   sudo mount 192.168.1.100:/mnt/shared /mnt/nfs
   ```
3. Add to `/etc/fstab` for auto-mount:
   ```sh
   192.168.1.100:/mnt/shared /mnt/nfs nfs defaults 0 0
   ```

## Best Practices
- Use **NFSv4** for better security and performance.
- Implement **Kerberos authentication** for secure access.
- Restrict access using **IP-based permissions** in `/etc/exports`.
- Enable **firewall rules** to allow only necessary clients.
- Regularly monitor NFS logs for security audits.

## Interview Questions and Answers
### Basic Questions
1. **What is NFS?**
   - NFS (Network File System) is a protocol that allows remote file sharing between Unix/Linux systems over a network.

2. **What are the differences between NFSv3 and NFSv4?**
   - NFSv4 is stateful, supports ACLs, better security, and performance improvements, while NFSv3 is stateless.

3. **What is the purpose of the /etc/exports file?**
   - It defines directories that are shared via NFS and specifies client access permissions.

4. **How do you check mounted NFS shares on a Linux client?**
   - Use the `mount -t nfs` or `df -hT` command.

5. **How do you troubleshoot NFS connectivity issues?**
   - Check network connectivity, firewall rules, NFS service status, and `/var/log/syslog` for errors.

### Scenario-Based Questions
1. **An NFS client is unable to access the mounted directory. How would you troubleshoot it?**
   - Check if the NFS service is running on the server (`systemctl status nfs-kernel-server`).
   - Verify client IP permissions in `/etc/exports`.
   - Ensure NFS ports are open on the firewall (`nfsstat -s`).
   - Restart the NFS service and remount the directory.

2. **How do you improve NFS performance?**
   - Use NFSv4, enable async writes, increase read/write buffer sizes, and optimize network configurations.

3. **How do you restrict NFS access to specific clients?**
   - Define client IP ranges in `/etc/exports` with specific permissions.

4. **What are some security risks in NFS, and how do you mitigate them?**
   - Risks: Unauthorized access, data interception.
   - Mitigation: Use Kerberos authentication, firewall rules, and encrypted VPN connections.

5. **How do you persist an NFS mount across reboots?**
   - Add an entry in `/etc/fstab` with proper mount options.

## References
- [NFS Documentation](https://linux.die.net/man/5/exports)

---

### Author
*G Pavan Kumar*  
[LinkedIn](https://linkedin.com/in/gajulapavankumar27) | [GitHub](https://github.com/MrSRE/GPavanKumar)

