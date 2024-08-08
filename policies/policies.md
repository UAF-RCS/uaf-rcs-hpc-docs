# Policies

## Principle Investigators

### **General Policies**

PIs are responsible for all activities relating to their project, including the activities of other project members. PIs are also responsible for meeting the licensing terms of any software or data that are used on RCS systems.

### **Subsidized Resources**

Each PI is given the following subsidized resources to share across all projects:

* 30 TB of tape storage on $ARCHIVE
* 1 virtual machine

### **Additional Resources**

If additional resources are required beyond what is subsidized, PIs should request funding for resources through their director or local business office. RCS will contact the PI if a project exceeds its resource quota and a 3-month grace period will be provided before resources are purged.

## All Users

### **General Policies**

Users of RCS systems agree to abide by published UAF policies and standards: [https://www.uaf.edu/nooktech/policies-standards/index.php](https://www.uaf.edu/nooktech/policies-standards/index.php). Every user of RCS systems may rightfully expect their programs, data, and documents stored on RCS systems to be inaccessible by others, secure against arbitrary loss or alteration, and available for use at all times. To help protect system security and achieve this goal, RCS staff reserve the right to routinely examine user accounts. In the event of a suspected security incident, RCS staff may inactivate and examine the contents of user accounts without prior notification.

### **Account Sharing**

Users of RCS systems may not share their account with anyone under any circumstances. This policy ensures every user is solely responsible for all actions from within their account. When shared access to a particular set of files on a system is desired, UNIX group permissions should be applied. Contact [uaf-rcs@alaska.edu](mailto:uaf-rcs@alaska.edu) for more information regarding changing group permissions on files and directories.

### **User-owned Files and Directories**

For home directories, RCS recommends authorizing write access to only the file/directory owner. Group and world write permissions in a home directory should be avoided under all circumstances.

For the $CENTER1 and $ARCHIVE filesystems, RCS recommends using caution when opening group and world read / execute permissions, and extreme caution when opening group and world write permissions.

Setuid and setgid permissions are prohibited on all user-owned files and directories.

User files may be scanned by RCS staff at any time for system security or maintenance purposes.

### **Passwords**

RCS uses University of Alaska \(UA\) credentials for user authentication. Therefore, passwords used to access RCS systems are subject to UA password guidelines. UA passwords may be changed using ELMO \([https://elmo.alaska.edu](https://elmo.alaska.edu/)\). If you suspect your password has been compromised, contact the UAF OIT Helpdesk \([helpdesk@alaska.edu](mailto:helpdesk@alaska.edu), 907-450-8300\) immediately.

### **SSH Public Keys**

Sharing of private SSH keys to allow another user to access an RCS account is considered account sharing and is prohibited on RCS systems.

Users of SSH public keys are responsible for their private keys and ensuring they are protected against access from other users. Private SSH keys should be generated and stored only on trusted systems.

### **System-generated E-mail**

RCS provides a ~/.forward file for users on each system. When the system generates an email, the message will be forwarded to email address\(es\) listed in the .forward file. Users are free to update their ~/.forward file to their preferred email address.

### **Respect Other Users**

Do not attempt to break passwords, tamper with system files, access files in other users' directories without permission, or otherwise abuse the privileges given to you with your RCS account. Your privileges do not extend beyond the directories, files, and volumes which you rightfully own or to which you have been given permission to access.

### **Software and Data License Agreements**

Users are responsible for meeting the license terms of any software or data that they install on RCS systems.

### **Restricted Services**

Research projects with data and software restricted by International Traffic in Arms Regulations \(ITAR\), National Institute of Standards and Technology \(NIST\), or other are asked to contact [uaf-rcs@alaska.edu](mailto:uaf-rcs@alaska.edu) for assistance. In addition, PI's should review Office of Research Integrity policies and procedures at [http://www.uaf.edu/ori](http://www.uaf.edu/ori).

### **Account Deactivation and Removal**

User accounts will be deactivated after a year of inactivity. RCS will notify the user and project's PI once the account is deactivated and give a 3-month grace period to transfer needed data out of the user's account before the user account's data is purged.

## Service Availability

### **Workstation Support Hours**

* Mac workstation support is available from 9:30 AM - 4:00 PM, Monday - Friday.
* Windows workstation support is available from 9:00 AM - 5:00 PM, Monday - Friday.

### **Chinook Maintenance Periods**

* Monthly: First Wednesday for non-interrupt Operating System security and Scyld ClusterWare updates
* Quarterly: First Wednesday of Jan, Apr, Jul, and Oct for Operating System and Scyld ClusterWare updates that may require system downtime
* Twice per year: The month of May during the Facility Annual Systems Testing and over the winter closure for Operating System and Scyld ClusterWare updates that may require system downtime

## Policy Enforcement

Abuse of RCS resources is a serious matter and is subject to immediate action. A perceived, attempted, or actual violation of standards, procedures, or guidelines pursuant with RCS policies may result in disciplinary action including the loss of system privileges and possibly legal prosecution in the case of criminal activity. RCS employs the following mechanisms to enforce its policies:

* Contacting the user via phone or email to ask them to correct the problem.
* Modifying the permissions on user's files or directories in response to a security violation.
* Inactivating accounts or disabling access to resources to ensure availability and security of RCS systems.

