# Kerberos KDC Bootstrapper

This utility will configure and create a local Kerberos KDC for use with
Cloudera Manager and CDH.

__WARNING__

The KDC provisioned by this utility is for testing and demo purposes only.
Specifically, the master key is no where near sufficient for a production
deployment of a KDC. No production security infrastructure should ever be
deployed without a complete understanding of the technology and configuration.

Requirements:

* A CentOS/Redhat Linux workalike distribution
* Root privileges
* Intermediate Linux knowledge
* Very basic Kerberos knowledge

## What it does

Here's what running the utility will do to your system:

1. Confirm it can run on your system by checking a bunch of environmental
   information.
1. Alert you that it __will__ make changes to any current Kerberos or KDC
   configuration. __Any existing Kerberos KDC will be replaced__, however the
   original files will be backed up.
1. Install Kerberos-related packages via Yum, if they're not already installed.
1. Generate the necessary configuration files and create a local MIT Kerberos
   KDC (usually under /var/kerberos/krb5kdc).
1. Generate a system-wide Kerberos configuration file (/etc/krb5.conf).
1. Create a Kerberos principal for Cloudera Manager (cloudera-scm/admin) so CM
   can be configured to manage Kerberos principals and keytabs for various CDH
   services.
1. If running on the same host as Cloudera Manager, generate the proper
   configuration files and keytabs for the CM server
   (/etc/cloudera-scm-server/{cmf.principal, cmf.keytab}).
1. Start the Kerberos KDC and Admin services.
1. Tell you where to find the documentation for enabling Kerberos in Cloudera
   Manager, and what to do next.

## Running

1. Decide if you need to modify any settings.

   In most cases, nothing needs to be changed. The hostname of the machine,
   however, is absolutely critical to proper functionality of Kerberos. The
   provisioned KDC will use (by default) the hostname produced by `hostname -f`
   and the domain name produced by `hostname -d`. The KDC realm is `CLOUDERA`.
   If you desperately want to change things, see the first few variables in
   `configure_krb5.sh`.

   If you want to adjust the generated configuration files, edit the templates
   found in the `tmpl` directory.

1. Run the following, as root:

    ./configure_krb5.sh

1. Follow directions to configure Cloudera Manager's Kerberos support, and
   configure services.
1. Create any additional Kerberos principals for users for testing.

## License

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

Copyright Cloudera 2013

