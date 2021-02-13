# Ansible

**This** cheat sheet **is NOT complete!**

## Modules

- _common_
  - backup_file (for backup param)
  - changed, failed, msg, rc, skipped, stderr, stderr_lines, stdout, stdout_lines
  - diff: [{ after after_header before before_header }, {after_header, before_header}]
  - invocation, results: {...}
- stat: checksum_algorithm=sha1 follow=no get_attributes=yes get_checksum=yes **path**
  - stat: atime attributes charset checksum ctime dev executable exists gid gr_name inode isblk ischr isdir isfifo isgid islnk isreg issock isuid lnk_source lnk_target md5 mimetype mode mtime nlink path pw_name readable rgrp roth rusr size uid wgrp woth writeable wusr xgrp xoth xusr

## Sources

- [Ansible - Documentation](https://docs.ansible.com/ansible/latest/index.html)
- Modules:
  - [ansible.builtin.stat – Retrieve file or file system status](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/stat_module.html)
