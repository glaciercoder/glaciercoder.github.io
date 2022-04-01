---
layout: default
title:  "Mac disk management"
date:   2022-03-23 12:07:36 +0800
categories: Mac
---



# Ref

http://www.theinstructional.com/guides/disk-management-from-the-command-line-part-2

# Basic concepts

In order to store data on a partition, it needs a filesystem. Once a partition has been formatted, this combination of partition and filesystem is known as a *volume*.

APFS: The Apple File System (APFS) allocates disk space on demand. When a single APFS container (partition) has multiple volumes, the container's free space is shared and can be allocated to any individual volume as needed. Each volume uses only a portion of the overall container, so that the available space is the total size of the container minus the size of all volumes in that container.