
# EaseFilter Java Demo
EaseFilter File Security SDK is a comprehensive solution designed for developers to implement file-level security, encryption, access control, and auditing directly within their applications. By integrating this SDK, developers can enforce data protection policies, monitor file operations in real time, and prevent unauthorized access across multiple environments.

This is a collection of simple CLI demos for [EaseFilter](https://easefilter.com).
The source code is thoroughly documented, and serves as an example for using EaseFilter.

Java 17 and above is supported.
**A license key is required** to use this program.
Contact [info@easefilter.com](mailto:info@easefilter.com)
for a trial key.

## Key Features
- **Transparent File Encryption**  
  Encrypt and decrypt files on-the-fly without requiring changes to existing applications.  
- **Granular Access Control**  
  Define and enforce file access policies based on user, process, and security attributes.  
- **Real-Time Monitoring**  
  Capture and log file operations such as read, write, delete, and rename in real time.  
- **Registry Filtering**  
  Monitor and control Windows registry operations with fine-grained rules.  
- **Digital Rights Management (DRM)**  
  Protect shared files with embedded access control policies and audit trails.  
- **Cross-Platform Support**  
  Works with FAT, NTFS, ReFS, and network shares, supporting Windows environments including Windows 10 and Server editions.  

## Benefits
- Enhance application security with minimal development effort.  
- Meet compliance requirements for data protection and auditing.  
- Prevent data leakage by enforcing strict file access and sharing policies.  
- Integrate seamlessly into existing workflows and enterprise systems.  

## Use Cases
- **Enterprise Data Protection**: Secure sensitive corporate files from unauthorized access.  
- **Cloud Security**: Protect files stored and accessed through cloud platforms.  
- **DRM & File Sharing**: Enforce digital rights when distributing confidential documents.  
- **Compliance & Auditing**: Generate detailed audit logs for regulatory compliance.  

## Installation

> [!NOTE]
> Administrator permissions are required to run EaseFilter.

- [Install Java.](https://learn.microsoft.com/en-us/java/openjdk/install)

- [Install Maven.](https://maven.apache.org/install.html)

- Edit the configuration file at `src\main\resources\config.properties` and add the license key.

- Compile the demo CLI:

  ```
  mvn package
  ```
  
- You can now run the demo:

  ```
  .\ef-demo --help
  ```

## Examples

Here are some examples of using the demo CLI.
These commands assume you are using `cmd` or `powershell`;
on a different shell, quote the arguments appropriately.

To get help with a specific subcommand, you may pass `--help` to it, for example

```
.\ef-demo monitor --help
```

to get help for using the monitor filter demo.

### Monitor filter

- Monitor all events in the filesystem:
  ```
  .\ef-demo monitor *
  ```

- Monitor all events in the `C:\` drive:
  ```
  .\ef-demo monitor C:\*
  ```
  
- Monitor all events in a specific directory:
  ```
  .\ef-demo monitor C:\path\to\directory\*
  ```
  
### Control filter

Deny all file writes in a directory:

  ```
  .\ef-demo control --block-perms="ALLOW_WRITE_ACCESS,ALLOW_OPEN_WITH_CREATE_OR_OVERWRITE_ACCESS" C:\path\to\directory\*
  ```
  
Deny all reads in the directory:

  ```
  .\ef-demo control --block-perms="ALLOW_READ_ACCESS" C:\path\to\directory\*
  ```

Deny file listing in a directory (makes directory seem empty):

  ```
  .\ef-demo control --block-perms="ALLOW_DIRECTORY_LIST_ACCESS" C:\path\to\directory\*
  ```

### Process filter

Monitor all process creations/deletions (try starting a PowerShell to test this):

  ```
  .\ef-demo process *
  ```

Monitor specifically `cmd.exe`:

  ```
  .\ef-demo process C:\Windows\System32\cmd.exe
  ```

Monitor all System32 processes:

  ```
  .\ef-demo process C:\Windows\System32\*
  ```

(BE CAREFUL with this flag) Prevent `cmd.exe` from starting:

  ```
  .\ef-demo process --deny C:\Windows\System32\cmd.exe
  ```

### Encryption filter

Transparently encrypt a directory:

  ```
  .\ef-demo encrypt C:\path\to\directory\*
  ```

This will prompt for a password to encrypt the directory with.
New files written to the directory will be encrypted.
Once the filter is stopped, files contents will be scrambled and unreadable.

> [!WARNING]
> In this simplified demo program, the encryption key is not generated securely.
> Use a proper key derivation method with a randomly-generated salt.

Encrypt a directory, and only allow Notepad to decrypt its contents:

  ```
  .\ef-demo encrypt --allow-proc notepad.exe C:\path\to\directory\*
  ```
  
### Registry filter

Monitor all registry events:

  ```
  .\ef-demo registry *
  ```

Monitor all registry events for keys with a matching name:

  ```
  .\ef-demo registry *KeyName*
  ```

Prevent deletion of keys with a matching name:

  ```
  .\ef-demo registry --block-perms=DELETE_KEY *KeyName*
  ```
  
Run `.\ef-demo registry --block-perms=HELP` to see a list of permissions that can be managed by EaseFilter.

## EaseFilter File System Filter Driver SDK Reference
| Product Name | Description |
| --- | --- |
| [Cloud File System SDK](https://www.easefilter.com/cloud/cloud-file-system-sdk.htm) | EaseFilter Cloud File System SDK Introduction. |
| [CloudTier Storage Tiering SDK](https://www.easefilter.com/cloud/storage-tiering-sdk.htm) | EaseFilter Storage Tiering Filter Driver SDK Introduction. |
| [File Monitor SDK](https://www.easefilter.com/kb/file-monitor-filter-driver-sdk.htm) | EaseFilter File Monitor Filter Driver SDK Introduction. |
| [File Control SDK](https://www.easefilter.com/kb/file-control-file-security-sdk.htm) | EaseFilter File Control Filter Driver SDK Introduction. |
| [File Encryption SDK](https://www.easefilter.com/kb/transparent-file-encryption-filter-driver-sdk.htm) | EaseFilter Transparent File Encryption Filter Driver SDK Introduction. |
| [Registry Filter SDK](https://www.easefilter.com/kb/registry-filter-drive-sdk.htm) | EaseFilter Registry Filter Driver SDK Introduction. |
| [Process Filter SDK](https://www.easefilter.com/kb/process-filter-driver-sdk.htm) | EaseFilter Process Filter Driver SDK Introduction. |
| [EaseFilter SDK Programming](https://www.easefilter.com/kb/programming.htm) | EaseFilter Filter Driver SDK Programming. |

## EaseFilter SDK Sample Projects
| Sample Project | Description |
| --- | --- |
| [CloudTier Storage Tiering Demo](https://www.easefilter.com/cloud/cloudtier-storage-tiering-demo.htm) | A HSM File System Filter Driver Demo. |
| [CloudTier S3 Tiering Demo](https://www.easefilter.com/cloud/cloudtier-s3-intelligent-tiering-demo.htm) | CloudTier S3 Intelligent Tiering Demo. |
| [Cloud File DR S3 Demo](https://www.easefilter.com/cloud/cloud-file-dr-demo.htm) | Cloud File DR S3 Demo. |
| [Amazon S3 File Explorer Demo](https://www.easefilter.com/cloud/s3-browser-demo.htm) | Amazon S3 File Explorer Demo. |
| [Auto File DRM Encryption](https://www.easefilter.com/kb/auto-file-drm-encryption-tool.htm) | Auto file encryption with DRM data embedded. |
| [Transparent File Encrypt](https://www.easefilter.com/kb/AutoFileEncryption.htm) | Transparent on access file encryption. |
| [Secure File Sharing with DRM](https://www.easefilter.com/kb/DRM_Secure_File_Sharing.htm) | Secure encrypted file sharing with digital rights management. |
| [File Monitor Example](https://www.easefilter.com/kb/file-monitor-demo.htm) | Monitor file system I/O in real time, tracking file changes. |
| [File Protector Example](https://www.easefilter.com/kb/file-protector-demo.htm) | Prevent sensitive files from being accessed by unauthorized users or processes. |
| [FolderLocker Example](https://www.easefilter.com/kb/FolderLocker.htm) | Lock file automatically in a FolderLocker. |
| [Process Monitor](https://www.easefilter.com/kb/Process-Monitor.htm) | Monitor the process creation and termination, block unauthorized process running. |
| [Registry Monitor](https://www.easefilter.com/kb/RegMon.htm) | Monitor the Registry activities, block the modification of the Registry keys. |
| [Secure Sandbox Example](https://www.easefilter.com/kb/Secure-Sandbox.htm) |A secure sandbox example, block the processes accessing the files out of the box. |
| [FileSystemWatcher Example](https://www.easefilter.com/kb/FileSystemWatcher.htm) | File system watcher, logging the file I/O events. |
| [ZeroTrust Example](https://www.easefilter.com/kb/zero-trust-file-access-control-demo.htm) | Zero trust file acc
ess control with encryption feature. |

## Filter Driver Reference

* [Understand MiniFilter Driver](https://www.easefilter.com/kb/understand-minifilter.htm)
* [Understand File I/O](https://www.easefilter.com/kb/File_IO.htm)
* [Understand I/O Request Packets(IRPs)](https://www.easefilter.com/kb/understand-irps.htm)
* [Filter Driver Developer Guide](https://www.easefilter.com/kb/DeveloperGuide.htm)
* [MiniFilter Filter Driver Framework](https://www.easefilter.com/kb/minifilter-framework.htm)
* [Isolation Filter Driver](https://www.easefilter.com/kb/Isolation_Filter_Driver.htm)

## Support
If you have questions or need help, please contact support@easefilter.com 

[Home](https://www.easefilter.com/) | [Solution](https://www.easefilter.com/solutions.htm) | [Download](https://www.easefilter.com/download.htm) | [Demos](https://www.easefilter.com/online-fileio-test.aspx) | [Blog](https://blog.easefilter.com/) | [Programming](https://www.easefilter.com/kb/programming.htm)
