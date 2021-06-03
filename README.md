ansible-tidy
============

Tidy role for Ansible, inspired by Puppet's tidy module. Remove unwanted files based on specific criteria.  
Multiple criteria are AND’d together
This is a fork of https://github.com/maxgalbu/ansible-tidy that works with Python 3

Installation
------------

This role isn't distributed using Ansible Galaxy.
Clone the repo under your roles folder instead.


New in version: 1.7

<table>
<tr>
<th class="head">parameter</th>
<th class="head">required</th>
<th class="head">default</th>
<th class="head">choices</th>
<th class="head">comments</th>
</tr>
<tr>
<td>tidy_age</td>
<td>no</td>
<td>0</td>
<td><ul></ul></td>
<td>Tidy files whose age is equal to or greater than the specified time.  
You can choose seconds, minutes, hours, days, or weeks by specifying the first letter of any of those words (e.g., ‘1w’). Specifying 0 will remove all files.</td>
</tr>
<tr>
<td>tidy_force</td>
<td>no</td>
<td></td>
<td><ul><li>yes</li><li>no</li></ul></td>
<td>Force removal of non empty directories</td>
</tr>
<tr>
<td>tidy_matches</td>
<td>no</td>
<td></td>
<td><ul></ul></td>
<td>One or more (shell type) file glob patterns, which restrict the list of files to be tidied to those whose basenames match at least one of the patterns specified.  
Multiple patterns can be specified using a list.</td>
</tr>
<tr>
<td>tidy_path</td>
<td>yes</td>
<td></td>
<td><ul></ul></td>
<td>Path to the file or directory to manage. Must be fully qualified.</td>
</tr>
<tr>
<td>tidy_recurse</td>
<td>no</td>
<td>no</td>
<td><ul><li>yes</li><li>no</li></ul></td>
<td>If target is a directory, recursively descend into the directory looking for files to tidy.</td>
</tr>
<tr>
<td>tidy_rmdirs</td>
<td>no</td>
<td>no</td>
<td><ul><li>yes</li><li>no</li></ul></td>
<td>Tidy directories in addition to files; that is, remove directories whose age is older than the specified criteria.  This will only remove empty directories, so all contained files must also be tidied before a directory gets removed.</td>
</tr>
<tr>
<td>tidy_silent</td>
<td>no</td>
<td>no</td>
<td><ul><li>yes</li><li>no</li></ul></td>
<td>Silently ignore failed commands.</td>
</tr>
<tr>
<td>tidy_size</td>
<td>no</td>
<td>0</td>
<td><ul></ul></td>
<td>Tidy files whose size is equal to or greater than the specified size.  
Unqualified values are in bytes, but b, k, m, g, and t can be appended to specify bytes, kilobytes, megabytes, gigabytes, and terabytes, respectively.  
Size is not evaluated for directories.</td>
</tr>
<tr>
<td>tidy_timestamp</td>
<td>no</td>
<td>atime</td>
<td><ul><li>atime</li><li>mtime</li><li>ctime</li></ul></td>
<td>Set the mechanism for determining age. Default is atime.</td>
</tr>
<tr>
<td>tidy_keep</td>
<td>no</td>
<td>0</td>
<td></td>
<td>Keep x files, delete all the others. Works with recurse, it will keep x files in each folder if recurse=yes. Files are ordered before tidying up, using the `tidy_timestamp` param, so you can delete older files. Specifying 0 will remove all files.</td>
</tr>
</table>  


* Playbook example:

```
---
- hosts: all

  roles:
    - role: maxgalbu.tidy

  vars:
    tidy_path: tests/files
    tidy_local_action: true
    tidy_recurse: true
    tidy_keep: 2
```
