---
title: Whitespace characters in file and folder names
description: Describes support for whitespace characters in file and folder names.
ms.data: 09/08/2020
author: Deland-Han
ms.author: delhan
manager: dscontentpm
audience: itpro
ms.topic: troubleshooting
ms.prod: windows-client
localization_priority: medium
ms.reviewer: kaushika
ms.prod-support-area-path: File Explorer/Windows Explorer
ms.technology: ShellExperience
---
# Support for Whitespace characters in File and Folder names for Windows 8, Windows RT and Windows Server 2012

This article describes support for whitespace characters in file and folder names.

_Original product version:_ &nbsp; Windows 10 - all editions, Windows Server 2012 R2  
_Original KB number:_ &nbsp; 2829981

## Summary

File and Folder names that begin or end with the ASCII Space (0x20) will be saved without these characters. File and Folder names that end with the ASCII Period (0x2E) character will also be saved without this character. All other trailing or leading whitespace characters are retained.

For example:

- If a file is saved as ' Foo.txt', where the leading character(s) is an ASCII Space (0x20), it will be saved to the file system as 'Foo.txt'.
- If a file is saved as 'Foo.txt ', where the trailing character(s) is an ASCII Space (0x20), it will be saved to the file system as 'Foo.txt'.
- If a file is saved as '.Foo.txt', where the leading character(s) is an ASCII Period (0x2E), it will be saved to the file system as '.Foo.txt'.
- If a file is saved as 'Foo.txt.', where the trailing character(s) is an ASCII Period (0x2E), it will be saved to the file system as 'Foo.txt'.
- If a file is saved as ' Foo.txt', where the leading character(s) is an alternate whitespace character, such as the Ideographic Space (0x3000), it will be saved to the file system as ' Foo.txt '. The leading whitespace characters are not removed.
- If a file is saved as 'Foo.txt ', where the trailing character(s) is an alternate whitespace character, such as the Ideographic Space (0x3000), it will be saved to the file system as 'Foo.txt '. The trailing whitespace characters are *not* removed.File and Folder names that begin or end with a whitespace character are enumerated differently by the Win32 and WinRT APIs due to ecosystem requirements.

## More information

##### Whitespace Characters

There are various whitespace characters representing various 'space' widths (glyphs). Only the ASCII Space (0x20) and ASCII Period (0x24) characters are handled specially by the Object Manager. Although the Ideographic Space character (0x3000) is also generated by using the Spacebar (when IME is enabled), it is not handled specially.
- 0x0020 SPACE
- 0x00A0 NO-BREAK SPACE
- 0x1680 OGHAM SPACE MARK
- 0x180E MONGOLIAN VOWEL SEPARATOR
- 0x2000 EN QUAD
- 0x2001 EM QUAD
- 0x2002 EN SPACE
- 0x2003 EM SPACE
- 0x2004 THREE-PER-EM SPACE
- 0x2005 FOUR-PER-EM SPACE
- 0x2006 SIX-PER-EM SPACE
- 0x2007 FIGURE SPACE
- 0x2008 PUNCTUATION SPACE
- 0x2009 THIN SPACE
- 0x200A HAIR SPACE
- 0x200B ZERO WIDTH SPACE
- 0x202F NARROW NO-BREAK SPACE
- 0x205F MEDIUM MATHEMATICAL SPACE
- 0x3000 IDEOGRAPHIC SPACE
- 0xFEFF ZERO WIDTH NO-BREAK SPACE

#### Object Manager

ASCII Space (0x20) characters at the beginning or end of a file or folder name are removed by the Object Manager upon creation.
ASCII Period (0x2E) characters at the end of a file or folder name are removed by the Object Manager upon creation.
All other leading or trailing whitespace characters are retained by the Object Manager.

#### API Enumeration

##### Win32 API

The Win32 API ([CreateFile](https://msdn.microsoft.com/library/windows/desktop/aa363858.aspx), [FindFirstFile](https://msdn.microsoft.com/library/windows/desktop/aa364418.aspx), etc.) uses a direct method to enumerate the files and folders on a local or remote file system. All files and folders are discoverable regardless of the inclusion or location of whitespace characters.

##### WinRT API

The WinRT API is designed to support multiple data providers (Physical Drives, OneDrive, Facebook, etc.). To achieve this, WinRT API uses a search engine to enumerate files and folders. Due to the search approach to enumeration, the WinRT API ([StorageFile](https://msdn.microsoft.com/library/windows/apps/windows.storage.storagefile.aspx), [StorageFolder](https://msdn.microsoft.com/library/windows/apps/windows.storage.storagefolder.aspx), etc.) does not handle file and folder names with trailing whitespace characters other than ASCII Space (0x20) and ASCII Period (0x2E) residing on a local or remote file system. It does handle leading non-ASCII whitespace characters.

### Observed Behavior

##### File Explorer and Desktop applications

All files and folders are visible within File Explorer and Desktop applications regardless of inclusion or location of whitespace characters.

##### Microsoft Store applications

When using the File Picker, files with a trailing non-ASCII whitespace character do not appear. The contents of subfolders with trailing non-ASCII whitespace characters are not displayed in the File Picker. Files or folders containing a leading non-ASCII whitespace character are displayed.