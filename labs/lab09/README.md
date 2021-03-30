# Lab 09: Authentication, Authorization, Accounting (AAA) and Proper Credential Management


Create a copy of this google document [lastname_lab09](https://docs.google.com/document/d/1xiAlbfG_8fXCWUxKg8Xqzn7hFUTO_Anp5xYGARpYInI/edit?usp=sharing) (File > Make a Copy) to record all of your assignment answers in.

The table of contents for this lab is found below.

Part 1. Accounting and auditing log files <br>
<!-- Part 2. Authentication and authorization flaws <br> -->
Part 2. Credential management and risks <br>
Part 3. Submission <br>

This week, we touch on a lot of important security concepts like (AAA) authentication, authorization, accounting, proper credentials and account management techniques and more! For this lab, we'll take a closer look at some of the concepts that we've discussed in lecture through a practical lens. Please make sure you have completed all of the material in the lessons tab before attempting this lab.

## Part 1 - Accounting and auditing log files

The below language is simply pulled from www.immersivelabs.com for your convenience. Please, read the information below and complete the [Accounting and Auditing](https://immersivelabs.online/labs/accounting-and-audit/) lab on immersive labs.


This module aims to provide a technical approach to understanding security accounting and auditing of log data, by combining the theoretical understanding of the process with a practical analysis of log data. As well as the process, we will cover available tools to facilitate accounting and auditing. Many of these are open-source, but those with enhanced features may be closed-source or proprietary software.

### Security accounting

Security accounting is the name of the process in which systems or applications generate log data (records of activity that can be reviewed later on). Examples of security accounting records include event logs from a Windows server/desktop computer and logs of network activity from a firewall.

In modern secure environments, security accounting data is processed centrally, enabling organisations to correlate and identify activities around an entire system or network.

### Security auditing

The process of reviewing security accounting records is known as security auditing. This is where accounting records are identified and suspicious activities can be reported. There are several other principles of security auditing, one being the separation of duties. This ensures that two or more parties are required to compromise security controls, making successful compromising less likely. This is achieved by disseminating the tasks and associated privileges for a specific security process among multiple people.

Another principle includes using an audit trail to prevent abuse of power or corruption of information. Broadly speaking, an audit trail is a system that traces the detailed transactions relating to any item in an accounting record. It also has a separate technical meaning, relating to a record of the changes that have been made to a database or file, yet both meanings are relevant to security. Audit trails fundamentally are used for performance monitoring, demonstration of adherence to a security policy, and detection and investigation of security policy breaches. For more information on security auditing regulations, see the Sarbanes Oxley Act 2002.

###  SIEM tools

The focus of this lab will be on tools that centralize accounting records and enable auditing (among other functions). These tools are known as Security Incident and Event Management (SIEM) tools.

There are many SIEM tools available for accounting and auditing, such as Splunk, LogRhythm, QRadar, and AlienVault OSSIM. Another is the Elastic Stack, which comprises of a range of tools that when working together, allow for the collation, storage, shipping, and analysis of data. As part of the Elastic Stack, Kibana is a visualization tool that facilitates analysis. A fully constructed and configured Elastic Stack is widely used as a SIEM tool, however, Elastic also offer the Elastic SIEM as an independent tool for real-time monitoring, which forms part of Elastic Security.

For more information on the Elastic Stack and an introduction on how to use it, check out our introductory labs below.

:interrobang: Question 1. Submit a screenshot of your badge demonstrating the completion of this immersive lab module.

<!-- ## Part 2 - Authentication and authorization flaws

The below language is simply pulled from www.immersivelabs.com for your convenience. Please, read the information below and complete the [Unrestricted File Upload](https://immersivelabs.online/labs/unrestricted-file-upload/category/offensive/series/authentication-and-authorisation-flaws) lab on immersive labs.

Unrestricted file upload is a vulnerability that occurs when insufficient checks are made on the file being uploaded. Thus, when weak security measures are implemented, an attacker can bypass them and upload their own code instead of the intended file (e.g., a PHP file when JPEG was expected). 

Once the file is successfully uploaded on the server, the attacker only needs to find a way to run it, leading to remote code execution. In the case of PHP and other server-side languages, navigating to the path of the file executes it on the server. 

In this module you must upload an image that enables you to take control of the server using a PHP shell, and then use that content to access the contents of /etc/token. More information on unrestricted file uploads can be found on the [OWASP website](https://owasp.org/www-community/vulnerabilities/Unrestricted_File_Upload).


:interrobang: Question 2. Submit a screenshot of your badge demonstrating the completion of this immersive lab module. -->

## Part 2 - Credential management and risks

The below language is simply pulled from www.immersivelabs.com for your convenience. Please, read the information below and complete the [Immersive Bank: Ep.1 – Open Source and Credentials](https://immersivelabs.online/labs/immersive-bank-episode-one-open-source-and-credentials/) AND [Immersive Bank: Ep.2 – Gaining Access](https://immersivelabs.online/labs/immersive-bank-episode-two-gaining-access/) modules on immersive labs.

### Immersive Bank: Ep.1 – Open Source and Credentials

:warning: You will need to use your answers from this module in the next module (Immersive Bank: Ep.2 – Gaining Access) of this series.

Welcome to episode one of the Immersive Bank module series. You've been employed by a large national bank who are looking to buy out a local company called IML Bank. The national corporation want you to test IML Bank's cybersecurity systems before they commit to the deal. Open source intelligence seems like a good place to start.

IML Bank has been the local bank for Immersive City for a number of years. The bank has been run by the same family since its creation; current CEO Carlo Fancini has been in this role since his mother stepped down. However, Immersive City is developing quickly and urbanizing rapidly, becoming a key economic player in the region. Now, a larger national bank is looking to buy IML Bank.

As part of the take over, the national bank has hired you to conduct some due diligence. You’ve been tasked with undertaking a technical offensive security exercise in order to fathom the level of cybersecurity within IML Bank’s systems. Prior to your investigation, you are informed that the bank doesn't use a domain controller (you’ll need this information for another episode).

Thanks to a data breach affecting a third party service the bank uses, you were able to retrieve a SHA256 hash of his password which could be of use. f1f7fa48b632e29fabf8bff8772076dbe1bed560f924146b7d8f044703514601

Starting with open source research into your target, you need to utilise different techniques to discover information from the bank's website (https://imlbank.info) and subsequent social media pages.

:interrobang: Question 2. Submit a screenshot of your badge demonstrating the completion of this immersive lab module.

### Immersive Bank: Ep.2 – Gaining Access

Welcome to episode two of the Immersive Bank module series. 

Credentials are key in this instalment of the series. Using the credentials you found in episode one, you'll now dig deeper into Immersive Bank's systems.

Thanks to your open source research, you know you can gain access to the CEO's computer. Using the credentials you discovered in episode one, you remotely connected to the computer in order to do some digging. You find some documents in a folder that could appear to be intriguing but without the password, you're unable to access them. 

Some interesting personal documents on the desktop pique your curiosity. It looks like Carlo mixes business with his personal life, leaving documents from his daughter's school easily accessible. Perhaps one of them can provide insight into the password protected files.

:interrobang: Question 3. Submit a screenshot of your badge demonstrating the completion of this immersive lab module.

## Part 3 - Submission

Convert your answer document in to a **.PDF** and upload a single `lastname_lab9.pdf` answer document containing all of your answers to the assignment questions to Brightspace through the attachment uploads option.
