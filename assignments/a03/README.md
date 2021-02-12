# Assignment 03: Basic Cyber Overview

Before attempting this assignment, please make sure you have completed all of the material in this weeks lessons.

Create a copy of this google document [lastname_A03](https://docs.google.com/document/d/1lyZrRlL8yveVshaKXLyR_cdOKFqGyxqnD-s0kxRxQEM/edit?usp=sharing) (File > Make a Copy) to record all of your assignment answers in.

Ensure your answer file has the following format:

The table of contents for this assignment is found below.

Part 1: Information Security <br>
Part 2: Why Hackers Hack <br>
Part 3: Who are the Hackers? <br>
Part 4: Cyber Attack Types <br>
Part 5: Cyber Attack Types <br>
Part 6: Cyber Attack Types <br>
Part 7: Cyber Attack Types <br>
Part 8: Submission <br>

# Lab 06: Walled Garden Network Architecture and Operating Systems

This week, we've  touch on some of the secure protocols that are used for secure communication. For this lab, we'll take a closer look at some of the architectures and operating systems discussed in lecture through a practical lens. Please make sure you have completed all of the material in the lessons tab before attempting this lab.

The table of contents for this lab is found below.

Part 1. NCSC Walled Garden Network Architecture <br>
Part 2. NTFS and Windows File Permissions <br>
Part 3. Submission <br>

Create a `lastname_lab06.docx` document to record all of your assignment answers in.

Ensure your answer file has the following format:

```text
Full Name
CSF 434/534 - Lab#06
Spring 2020

Question 1:
-----------
<your solution here>


Question 2:
-----------
<your solution here>

...
```

## Part 1 - NCSC Walled Garden Network Architecture

The below language is simply pulled from www.immersivelabs.com for your convenience. Please, read the information below and complete the [NCSC Walled Garden Network Architecture](https://dca.immersivelabs.online/labs/ncsc-walled-garden-network-architecture/) lab on immersivelabs.

> The resolution of this lab seems to be a little tricky. Zoom in or out by using the `+` or `-` icons in the immersive lab platform so each element of the Walled Garden Network Architecture is not sitting on top of each other.  Additionally, you can zoom in or out of the page itself with `ctrl (or cmd)` + `+` or `ctrl (or cmd)` + `-`. Using both zoom features of immersive lab and your browser should result in the following view of the architecture.

<img src="images/fig1.png">

As you can see in the above image, you can click on a node in the architecture to populate the host information pane on the bottom of this interface.

While this architecture has been deprecated and should not be deployed as a remote access solution in practice ~ we can still use it as an educational tool.

#### Quick Summary

Companies will often perform penetration tests against their networks, and the results can be both overwhelming and confusing. Understanding what is a priority and what isn’t can be challenging as, ultimately, this is subjective. In this lab, we will be looking at the penetration test results of a company’s remote-access solution.

#### Vulnerabilities, threats, and risks

As companies develop, they must ensure their networks are suitable for purpose. This means they must support customers, remote workers, email, and all manners of internal traffic. When a developing network is combined with software that rapidly becomes out of date, it is likely that vulnerabilities will soon appear.

These vulnerabilities need to be identified and assessed, with the outcome likely being remediation; however, a lack of cost, time, and expertise means that some security concerns will be written off as residual risk.

organizations will often hire external security consultants to perform penetration tests and vulnerability assessments. The results of these tests will then be scrutinised and acted upon as part of the vulnerability management process.

As part of the vulnerability management process, decisions regarding the remediation priority should be established. This will require the team to understand the impact of a vulnerability within the context of the affected network, taking into consideration the business requirements, accessible data as well as the impact and likelihood of exploitation.

#### Vulnerability Management

Vulnerability management is an ongoing procedure that aims to program and strategise a process, which allows the company to manage flaws in their system in an ongoing and holistic manner, without drastically affecting the day-to-day operations as a whole. Factors such as cost, disruption and compatibility must be considered when managing vulnerabilities.

This is not to be confused with vulnerability assessment, which looks at the security posture of a company as a whole from an external perspective, often carried out as a ‘one-off’ project over the course of a few months. 

[NCSC Vulnerability Management Guidance](https://www.ncsc.gov.uk/guidance/vulnerability-management)

## In this section of lab

In this section of lab, we will look at the results of a penetration test of the fictitious IML Bank’s remote-access solution. The company hosts all its own hardware and took the decision to base its solution on the Walled Garden Architecture, which was designed and released by the National Cyber Security Centre (NCSC), formerly known as Communications-Electronics Security Group (or CESG).

Within the network diagram, you will be able to select nodes to retrieve further information about the firewall rules, operating system and other information (such as version numbers and the data that is present).

Traversing the network will allow you to understand the scope of vulnerabilities and compare their Common Vulnerability Scoring System (CVSS) versus the real-world impact the vulnerability would have if exploited. 

You will be required to select the top three priorities for remediation, based on their impact within the context of the network. Once you have selected three issues with high enough weighting, you will be given the token as well as the option to see how we have weighted the issues.

#### Walled Garden

The Walled Garden network design aims to allow remote computers to gain access to selected services which are hosted within a company’s network, without presenting their core network to the remote user. Putting these remote computers in a protected zone ensures that if an endpoint is compromised, the damage that is inflicted on the network as a whole is limited. 

:interrobang: Question 1. Submit a screenshot of your badge and immersive lab username demonstrating the completion of this immersivelab module.


## Part 2 - NTFS and Windows File Permissions

The below language is simply pulled from www.immersivelabs.com for your convenience. Please, read the information below and complete the [Windows File Permissions](https://dca.immersivelabs.online/labs/windows-file-permissions/) lab on immersivelabs.

#### Quick Summary

This part of lab is about developing and validating the skills needed when using Windows NTFS file permissions. 

The NTFS (New Technology File System) is a proprietary file system developed by Microsoft and first staged in 1993, starting with Windows NT 3.1., the default file system for the Windows NT family. 

NTFS brought several technical improvements to the file systems it superseded (such as File Allocation Table [FAT] and High Performance File System [HPFS]). These improvements included features like improved support for metadata, and advanced data structures to enhance performance, reliability and disk-space use. 

Additional extensions include a more elaborate security system that is based on **Access Control Lists (ACLs)** and file system journaling. In NTFS, each file or folder is assigned a security descriptor that defines its owner and contains two ACLs. 

The first ACL is called **Discretionary Access Control List (DACL**) and it defines exactly what type of interactions (e.g. reading, writing, executing or deleting) are allowed or forbidden by a user or group of users.

For example, this could mean that files in the 'C:Program Files' folder may be read and executed by all users but can only be modified by a user holding administrative privileges. Windows Vista adds mandatory access control info to DACLs. DACLs are the primary focus of User Account Control for Windows Vista onwards. 

The second **ACL, System Access Control List (SACL)**, defines which interactions within the file or folder are to be audited and whether they should be logged when the activity is successful, failed or both. Auditing can be enabled on a company’s sensitive files so that managers can ascertain when someone tries to delete or copy files and if they succeed. 

In this exercise you will have access to a Windows Server to identify Windows drives as well as folder and file permissions. 

**Search terms**: NTFS ACLs, NTFS SACLs, NTFS permissions ownership, viewing. hidden files

#### External Links

[NTFS - Wikipedia](https://en.wikipedia.org/wiki/NTFS)

:interrobang: Question 2. Submit a screenshot of your badge and immersive lab username demonstrating the completion of this immersive lab module.


## Part 3. Submission

Convert your answer document in to a **.PDF** and upload a single `lastname_lab6.pdf` answer document containing all of your answers to the assignment questions to Sakai through the attachment uploads option.
