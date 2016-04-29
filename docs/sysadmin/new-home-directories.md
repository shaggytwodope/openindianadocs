# New Home Directories for new users

These are normally stored in ```/export/home/username``` but ```mounted``` to ```/home``` by a service called ```autofs```.

Once you've [created a ```user```](create-a-user.md) and their ```home folder``` (and given the user ```ownership``` of this folder) you will need to update the ```automount``` script. This is it before the addition.

```bash
adrian@openindiana-tuts:~$ cat /etc/auto_home
#
# Copyright 2005 Sun Microsystems, Inc.  All rights reserved.
# Use is subject to license terms.
#
# CDDL HEADER START
#
# The contents of this file are subject to the terms of the
# Common Development and Distribution License, Version 1.0 only
# (the "License").  You may not use this file except in compliance
# with the License.
#
# You can obtain a copy of the license at usr/src/OPENSOLARIS.LICENSE
# or http://www.opensolaris.org/os/licensing.
# See the License for the specific language governing permissions
# and limitations under the License.
#
# When distributing Covered Code, include this CDDL HEADER in each
# file and include the License file at usr/src/OPENSOLARIS.LICENSE.
# If applicable, add the following below this CDDL HEADER, with the
# fields enclosed by brackets "[]" replaced with your own identifying
# information: Portions Copyright [yyyy] [name of copyright owner]
#
# CDDL HEADER END
#
# ident "%Z%%M% %I%     %E% SMI"
#
# Home directory map for automounter
#
adrian  localhost:/export/home/&
+auto_home

```

To do this(open your favourite editor):

```bash
adrian@openindiana-tuts:~$ sudo nano /etc/auto_home # append paul localhost:/export/home/& before +auto_home
```

where paul is the ```user``` and ```home directory``` name.

It should now look like:

```bash
#
# Copyright 2005 Sun Microsystems, Inc.  All rights reserved.
# Use is subject to license terms.
#
# CDDL HEADER START
#
# The contents of this file are subject to the terms of the
# Common Development and Distribution License, Version 1.0 only
# (the "License").  You may not use this file except in compliance
# with the License.
#
# You can obtain a copy of the license at usr/src/OPENSOLARIS.LICENSE
# or http://www.opensolaris.org/os/licensing.
# See the License for the specific language governing permissions
# and limitations under the License.
#
# When distributing Covered Code, include this CDDL HEADER in each
# file and include the License file at usr/src/OPENSOLARIS.LICENSE.
# If applicable, add the following below this CDDL HEADER, with the
# fields enclosed by brackets "[]" replaced with your own identifying
# information: Portions Copyright [yyyy] [name of copyright owner]
#
# CDDL HEADER END
#
# ident "%Z%%M% %I%     %E% SMI"
#
# Home directory map for automounter
#
adrian  localhost:/export/home/&
paul    localhost:/export/home/&
+auto_home

```

Then start and stop the service:

```bash
adrian@openindiana-tuts:~$ sudo svcadm disable autofs
adrian@openindiana-tuts:~$ sudo svcadm enable autofs
```

Now when you login as that user their home directory will be automounted into the ```/home``` folder.

credit for these docs go to [/u/127b](https://www.reddit.com/user/127b)
