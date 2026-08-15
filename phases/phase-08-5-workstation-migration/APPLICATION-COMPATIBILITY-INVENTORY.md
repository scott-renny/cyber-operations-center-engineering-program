# Phase 8.5 Application Compatibility Inventory

> **Status:** Required before installation  
> **Public evidence:** Product categories and decisions only; licenses, account names, and private data remain private

## Purpose

Prevent a Linux Mint installation from stranding an essential Windows workflow. Every required application must have a tested disposition before the Windows workstation is sanitized.

## Decision categories

| Category | Preferred use |
|---|---|
| Native Mint/Ubuntu package | First choice when maintained in the supported repositories or by the verified upstream publisher |
| Flatpak | Desktop application delivered through a reviewed Linux Mint or Flathub source |
| Web application | Browser-based workflow with protected authentication |
| Linux replacement | Different product that satisfies the documented requirement |
| Windows virtual machine | Isolated exception for a justified Windows-only workload |
| Compatibility layer | Narrow exception after security and functionality testing |
| Retire | Unneeded, unsafe, obsolete, or unsupported software |

## Inventory template

| Windows application or workflow | Business or lab requirement | Linux Mint disposition | Data/configuration needed | Validation test | Decision |
|---|---|---|---|---|---|
| Browser and bookmarks | Web access | Native browser; import only reviewed bookmarks | Bookmarks, not full Windows profile | Sign-in and extension review | Pending |
| Password manager | Credential access | Verified Linux package or Flatpak | Account recovery material retained privately | Hardware-key and recovery test | Pending |
| Git and development tools | Engineering | Mint/Ubuntu packages and isolated environments | Repositories and reviewed configuration | Clone, build, and commit test | Pending |
| Office documents | Productivity | Native or web office workflow | Documents only | Open, edit, export, print | Pending |
| Video and streaming tools | Media | Native or Flatpak applications | Reviewed project/config files | Capture and export test | Pending |
| Virtual machines | Lab work | KVM/libvirt or reviewed VirtualBox support | Scanned VM disks and definitions | Boot, network isolation, snapshot | Pending |
| Windows-only workload | Exception | Replacement, VM, compatibility layer, or retire | Minimum required data | Functional and security test | Pending |

## Rules

- Do not copy installed Windows program directories as applications.
- Do not restore registry hives, scheduled tasks, services, browser caches, or the complete AppData tree.
- Reinstall software only from Mint/Ubuntu repositories, reviewed Flatpak remotes, or verified upstream publishers.
- Treat Wine or Bottles as an exception, not the default migration method.
- Prefer a disposable or isolated Windows VM for an unavoidable Windows-only tool.
- Import old virtual machines only after malware scanning and network-isolation review.
- Record license and recovery information privately before retirement.
- Do not sanitize the Windows workstation until every Required entry is validated or explicitly accepted as deferred.
