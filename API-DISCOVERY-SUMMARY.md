# Synology DSM API Discovery Summary

**Date:** 2025-11-28  
**Status:** In Progress

---

## Resources Found

### Official Synology Documentation
1. **FileStation API Guide** (PDF)
   - URL: https://global.download.synology.com/download/Document/Software/DeveloperGuide/Package/FileStation/All/enu/Synology_File_Station_API_Guide.pdf
   - Coverage: Complete FileStation API reference

2. **DSM Login Web API Guide** (PDF)
   - URL: https://global.download.synology.com/download/Document/Software/DeveloperGuide/Os/DSM/All/enu/DSM_Login_Web_API_Guide_enu.pdf
   - Coverage: Authentication and session management

3. **Surveillance Station Web API v2.0** (PDF)
   - Referenced in forums and official samples
   - Coverage: Camera management, recording, events

4. **Virtual Machine Manager API Guide** (PDF)
   - Referenced in terraform-provider-synology
   - Coverage: VM management

### GitHub Repositories Cloned

1. **N4S4/synology-api** ✅
   - Language: Python
   - Coverage: 300+ APIs, 29 modules
   - Status: Most comprehensive Python library
   - Modules: FileStation, DownloadStation, SurveillanceStation, Core APIs, Docker, Photos, VPN, etc.

2. **mib1185/py-synologydsm-api** ✅
   - Language: Python (async)
   - Coverage: Core DSM APIs
   - Status: Actively maintained, used by Home Assistant

3. **atom2ueki/mcp-server-synology** ✅
   - Language: Python (MCP server)
   - Coverage: FileStation, DownloadStation
   - Status: Modern MCP implementation

4. **zeichensatz/SynologyPhotosAPI** ✅
   - Language: Documentation
   - Coverage: Synology Photos API (unofficial)
   - Status: Community-documented

5. **synology-community/terraform-provider-synology** ✅
   - Language: Go
   - Coverage: FileStation, VMM, Core APIs
   - Status: Terraform provider with API references

6. **SynologyOpenSource/Synology-Surveillance-API-Samples** ✅
   - Language: Python
   - Coverage: Official Surveillance Station samples
   - Status: Official Synology repository

7. **pspete/pSynology** (not cloned yet)
   - Language: PowerShell
   - Coverage: DSM 6.x API endpoints
   - Status: PowerShell module

8. **plneto/Synology.Api.Client** (not cloned yet)
   - Language: C#/.NET
   - Coverage: FileStation, Auth
   - Status: .NET client library

---

## API Categories Discovered

### Core DSM APIs (SYNO.Core.*)
- System Information
- User Management
- Group Management
- Package Management
- Certificate Management
- Network Configuration
- File Services (SMB, AFP, NFS, FTP, SFTP)
- Hardware Control
- Event Scheduler
- Directory Services (LDAP, Domain)
- Notification Services

### FileStation (SYNO.FileStation.*)
- File/Folder Operations
- Upload/Download
- Search
- Sharing
- Compression/Extraction
- Background Tasks
- Favorites
- Virtual Folders
- MD5 Checksums
- Directory Size Calculation

### DownloadStation (SYNO.DownloadStation.*)
- Task Management
- RSS Feeds
- BT Search
- Statistics
- Scheduling

### Surveillance Station (SYNO.SurveillanceStation.*)
- Camera Management
- Recording
- Events
- Live View
- PTZ Control
- Home Mode

### ActiveBackup (SYNO.ActiveBackup.*)
- Device Backup
- Task Management
- Version Management
- Restore Operations
- AEM (Apple Enterprise Management)
- VM Backup (VMware, Hyper-V)

### Photos (SYNO.Foto.*, SYNO.FotoTeam.*)
- Album Management
- Photo Browsing
- Sharing
- Search

### Docker (SYNO.Docker.*)
- Container Management
- Image Management
- Network Management

### VPN (SYNO.Core.Network.VPN.*)
- L2TP
- OpenVPN
- PPTP

### Storage (SYNO.Core.Storage.*)
- Volume Management
- Share Management
- Snapshot Management
- RAID Configuration

---

## Next Steps

1. ✅ Clone all major GitHub repositories
2. ⏳ Extract complete API endpoint list from all sources
3. ⏳ Test endpoints against live Synology NAS (192.168.20.11)
4. ⏳ Document working endpoints with examples
5. ⏳ Organize documentation by application/package
6. ⏳ Create comprehensive API reference similar to UniFi docs

---

## API Coverage Statistics

### From synology-api Library (N4S4)
- **Total Modules:** 35
- **Total Methods:** 905+
- **FileStation Methods:** 46
- **DownloadStation Methods:** 24
- **SurveillanceStation Methods:** ~100+
- **Core APIs Methods:** ~200+
- **Other Apps:** ~535+

### Currently Documented
- **ActiveBackup:** 35 APIs, 215 methods ✅
- **FileStation:** 5 categories, 46 methods ⏳ (in progress)
- **DownloadStation:** Not started
- **Core DSM:** Not started
- **Surveillance:** Not started

### Target
- Document all major DSM APIs with working examples
- Test all endpoints against live NAS (192.168.20.11)
- Organize by application/package
- Provide Python, curl, and real-world examples

