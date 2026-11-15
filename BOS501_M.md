# Mini Literature Review: OS-Level Logging, Tracing, and Access Control Support for Data Integrity in Chromatography Data Systems
**Group Members**: Bassema Moustafa (bassema_222036, C1), Fatima Bayon (fatima_256825, C1), 
Lelas Khabbaz (lailas_khabaz_243474, C3), Oula Hatahet(oula_213054, C6)
**General Topic No. & Title**: 26. Operating system logging, tracing, and observability mechanisms.
**Specific Focus**: The role of system calls tracing, user-space interception, and user-space I/O logging in OS-levels.
**Word count (main body)**: about 3000 word
## 1. Abstract
Chromatography data systems (CDSs) generate and manage critical electronic records used in pharmaceutical quality control. 
Maintaining the integrity of these records requires not only reliable application software and analytical instruments, but also effective operating-system controls. 
This literature review examines the role of operating-system-level logging, tracing, access control, and observability in supporting data integrity in CDS environments. 
It focuses on critical operating-system events, including kernel activity, authentication, process and service behavior, file-system changes, device communication, and security events. 
The review also examines mechanisms such as system-call monitoring, kernel tracing, binary rewriting, tamper-evident logging, and live trace reconstruction.
The literature indicates that these mechanisms can help prevent privilege escalation, detect unauthorized changes, reconstruct system activity, and investigate failures affecting data acquisition, processing, and storage. 
However, the reviewed studies are mainly conducted in general-purpose or Linux-based environments and provide limited evidence regarding their integration with validated, Windows-based chromatography data systems. 
The findings support a layered approach that combines operating-system protection, protected logging, tracing, file-integrity monitoring, application audit trails, and risk-based validation. 
Future research should evaluate the performance, compatibility, regulatory suitability, and practical implementation of these controls in real CDS environments.
## 2. Introduction and Research Questions
The term “decision” may be represented by the phrase *Data Evaluation Creates Insights for Successful In-Process Operations and Next Steps*. 
This reflects the essential role of data in decision-making and highlights the importance of data integrity in ensuring reliable and defensible decisions. 
Between 2012 and 2016, the United States Food and Drug Administration (FDA) issued 66 warning letters concerning data-integrity violations; approximately 62% of the cited deficiencies were related to laboratory practices [1].
**RQ1:** Which operating-system-level events are identified as critical or relevant for monitoring data integrity in chromatography data systems?
**RQ2:** What operating-system-level mechanisms are proposed or used to support data integrity in chromatography data systems, and how do these mechanisms operate?
**RQ3:** What challenges and limitations affect the completeness, security, reliability, and tamper-resistance of operating-system audit logs in chromatography data systems?
## 3. Background and Core Concepts
Compliance with current Good Manufacturing Practice (cGMP) requirements and 21 CFR Part 11 is essential for ensuring that pharmaceutical products consistently meet their intended specifications and remain safe, effective, and free from contamination or defects [1]. 
Manufacturing and testing activities generate large volumes of electronic data, including instrument readings, sample information, processing parameters, calculations, reports, and audit records [2].
The reliability of this data is therefore fundamental to both product quality and regulatory compliance [1,2,10].
**Chromatography Data Systems:**
Chromatography data systems (CDSs) support many operations associated with chromatographic instruments, including data recording, sample scheduling, process-parameter control, signal processing, and final-result calculation [2]. 
These operations can be considered across three connected stages: the movement of data between instruments and software, the processing and interpretation of measurements, and the storage of original data and derived results. 
A failure at any stage may affect the reliability of the final analytical record [1.2].
**Data Integrity:** 
Data integrity refers to the completeness, consistency, and accuracy of data throughout its lifecycle. 
Under the ALCOA principles, data should be attributable, legible, contemporaneously recorded, original or a true copy, and accurate [3]. 
The extended ALCOA+ principles further emphasize that data should publication date, academic credibility, relevance to operating systems, and availability of full-text informatioalso be complete, consistent, enduring, and available [3]. 
These requirements apply not only to the CDS application, but also to the operating environment in which the system depends [4].
**Operating System Events:**
The operating system (OS) coordinates the processes, threads, files, storage resources, instrument interfaces, network connections, user authentication, permissions, and system services required for reliable CDS operation [2,7]. 
Consequently, OS failures or unauthorized changes can affect the completeness, accuracy, consistency, and traceability of chromatographic records. 
OS-level logging, tracing, access control, and monitoring therefore provide important supporting controls for detecting abnormal activity, reconstructing events, limiting unauthorized actions, and investigating potential data-integrity problems [5,6].
**Operating-System Logging:**
OS logs provide a record of events occurring within the computing environment. 
Kernel events can help determine whether an incomplete acquisition or corrupted result was caused by hardware or operating-system failure rather than by the CDS application. 
Authentication records successful and failed logins, session activity, password changes, account lockouts, privilege elevation, and remote access, thereby supporting user accountability [7]. 
Process and service logs record program execution, service failures, interruptions, and restarts; this information may explain missing data when a database, licensing, backup, synchronization, or instrument-communication service becomes unavailable [7]. 
File-system logs record the creation, modification, deletion, renaming, and permission changes of files and directories, helping identify accidental deletion or unauthorized modification of chromatograms, methods, reports, audit records, and backups [8].
**Operating-System Tracing:**
Tracing complements event logging by showing how the system behaves internally rather than simply indicating that an event occurred. 
It can reveal the sequence and timing of operations, such as whether an acquisition process opened the correct data file, wrote measurements to storage, communicated with an instrument driver, or terminated unexpectedly [8,9]. 
System-call, kernel, process, network, and file-system tracing, together with technologies such as Event Tracing for Windows, Linux ftrace, and eBPF, can therefore assist in identifying the precise causes of incomplete acquisitions, communication errors, and storage failures [8].
Observability and performance monitoring:
Observability brings logs and traces together with system metrics to provide a broader understanding of system behavior. 
Relevant OS-level metrics include CPU utilization, memory consumption, disk latency, network performance, process status, service availability, and file-system capacity. 
These measurements can reveal insufficient storage, slow disk operations, memory exhaustion, excessive processor load, interrupted network communication, or unavailable services before or during an analytical run. 
When appropriately configured and correlated with application records and instrument data, OS-level observability supports faster troubleshooting and strengthens confidence in the integrity and reliability of chromatographic results [7,8].
**OS-Level Mechanisms:**
**Detection, accountability, and response:**
Audit logging and event monitoring record important system and security activities. These may include login attempts, file access, privilege changes, process creation, and configuration changes. 
Examples include Linux audit logs, Windows Security Event Logs, and macOS Unified Logging. Real-time monitoring and alerting detects suspicious activity while it is happening. 
The system can notify administrators or automatically respond to events such as repeated failed logins, unauthorized file changes, or unusual process behavior. 
Secure timekeeping and timestamp protection ensure that system timestamps are accurate and difficult to manipulate. Accurate time is important for correlating audit events and investigating incidents. 
Secure Network Time Protocol, protected system clocks, and restricted time-change permissions are common examples [7,14].
**Identity, authorization, and privilege:**
Authentication and access control verify the identity of users and decide what resources they may access. 
Examples include passwords, multifactor authentication, certificates, user groups, access-control lists, and role-based access control. 
Privilege separation and least privilege ensure that users, applications, and services receive only the permissions they need. 
This limits the damage caused by mistakes or compromised accounts. 
Examples include standard user accounts, sudo, Windows User Account Control, service accounts, and Linux capabilities[7,14,17,18].
**Data and storage protection:**
File and directory protection prevents unauthorized reading, modification, deletion, or execution of stored data. 
Operating systems use file ownership, permissions, access-control lists, security labels, and encrypted directories for this purpose. 
Cryptographic integrity verification detects unauthorized or accidental changes to files, software, and system components. 
Common techniques include cryptographic hashes, message authentication codes, digital signatures, signed software packages, Secure Boot, and file-integrity monitoring. 
Secure I/O and storage handling protects information while it is being transferred, processed, or stored. 
Examples include disk encryption, secure deletion, encrypted swap space, controlled device access, protection against unauthorized direct memory access, and safe handling of temporary files [7,14].
**Execution and system isolation:**
Process and service isolation limits the ability of one program or service to interfere with another. 
Isolation reduces the effects of software failures and security breaches. Examples include sandboxes, containers, virtual machines, namespaces, control groups, restricted system calls, and security frameworks. 
Operating-system hardening and configuration control reduce the system’s attack surface and keep its security settings consistent. 
This includes applying security patches, disabling unused services, configuring firewalls, enforcing secure baselines, controlling software installation, protecting the kernel, and managing configuration changes [7,17].
**Continuity and historical preservation:**
Backup, recovery, and retention mechanisms allow organizations to restore systems and data after failures, attacks, corruption, or accidental deletion. 
Examples include encrypted backups, offline backups, immutable backup copies, snapshots, versioned backups, recovery images, tested restoration procedures, and retention policies. 
Together, these mechanisms protect the operating system by controlling access, limiting privileges, protecting data, isolating processes, detecting suspicious behavior, preserving evidence, and supporting recovery after an incident [7,14,18].
## 4. Literature Synthesis
These literatures present data integrity as a layered challenge involving operating-system security, system observability, tamper-evident logging, and pharmaceutical quality management. Rather than treating these areas independently, the studies collectively suggest that reliable data protection requires controls capable of preventing unauthorized actions, recording system activity, reconstructing events, and demonstrating compliance with quality requirements.
*Load-Time Selective Binary Rewriting* theme is the protection of operating-system privileges and process behavior. 
Research on the Additional Kernel Observer focuses on detecting unauthorized privilege changes during system-call execution, thereby preventing privilege-escalation attacks that could allow an attacker to control system resources or manipulate protected data. 
Similarly, SaBRe demonstrates how selective binary rewriting can intercept system calls and functions at load time, supporting monitoring, fault injection, and controlled modification of program behavior. Together, these studies show that system calls and process execution provide important control points for detecting or restricting potentially harmful activity [10].
*Combining Storage-Based And Ratcheting For Tamper-Evident Logging* theme concerns the preservation and reconstruction of trustworthy evidence. 
SealFSv2 addresses tamper-evident logging by combining storage-based protection with ratcheting mechanisms, helping ensure that recorded events cannot be silently modified or removed [11]. Live system-call trace reconstruction complements this approach by reconstructing process behavior from system-call activity[12]. 
These techniques provide more detailed evidence than conventional event logs because they can reveal the sequence of operations involving files, storage, processes, and system resources. This capability is valuable when investigating incomplete acquisitions, unexpected process termination, or unauthorized data changes.
*Data Integrity in Pharmaceutical Quality System* literature provides the regulatory and organizational context for applying these technical mechanisms. 
It emphasizes that data must remain accurate, complete, consistent, attributable, and available throughout its lifecycle [13]. 
Technical controls have described in *Additional kernel observer: privilege escalation attack prevention mechanism focusing on system call privilege* such as privilege monitoring, protected logging, and system-call tracing can support these requirements, but they must be incorporated into validated computerized systems, access-control procedures, audit trails, and quality-management practices [14,15]. 
Therefore, operating-system security should be viewed as a supporting layer within a broader pharmaceutical data-integrity framework [4,9].
Overall, the literature supports a defense-in-depth model. 
Kernel-level mechanisms provide prevention, binary rewriting and tracing provide observation, tamper-evident logging provides trustworthy evidence, and pharmaceutical quality systems provide validation and governance [16]. 
However, the studies largely examine general-purpose or Linux-based environments and do not establish how these mechanisms can be integrated into chromatography data systems, many of which operate on Windows and depend on specialized instruments and drivers [16]. 
Future research should therefore evaluate compatibility, performance, validation requirements, and regulatory suitability of combined operating-system controls in real CDS environments. 
## 5. Comparison / Analysis Table
| Aspect | Technique A: OS-Level Protection and Rewriting | Technique B: Logging, Tracing, and Tamper Evidence | Technique C: Pharmaceutical Data-Integrity Controls | Insights |
|---|---|---|---|---|
| Representative papers | SaBRe; Additional Kernel Observer (AKO) | SealFSv2; Live System Call Trace Reconstruction on Linux | Patel & Rajgor; Koumandaros; Integrated Laboratory Informatics Systems | The papers address different layers of system reliability and data integrity. |
| Objective | Prevent privilege escalation and selectively modify or intercept program behavior. | Record, reconstruct, and protect system activity against tampering. | Ensure reliable pharmaceutical data through quality systems, validation, and laboratory informatics. | Technical controls must support both security and regulated operational requirements. |
| Technique | Kernel observation, system-call monitoring, load-time binary rewriting, and plug-in-based interception. | Storage-based and ratcheting logs, system-call tracing, and forensic reconstruction. | Risk-based validation, procedural controls, quality-system practices, and integrated laboratory systems. | Prevention, detection, and governance are complementary rather than interchangeable. |
| Operating-system focus | Strong focus on kernel behavior, process privileges, system calls, and binary execution. | Focus on Linux logging, system calls, storage, and event reconstruction. | Limited direct OS-level analysis; emphasis on computerized systems and laboratory operations. | Pharmaceutical studies should examine OS mechanisms more explicitly. |
| Protection against unauthorized changes | AKO detects unexpected privilege changes; SaBRe can control or intercept selected operations. | SealFSv2 provides tamper-evident logging, while tracing can expose suspicious activity. | Validation, access control, and procedures reduce the likelihood of unauthorized or accidental changes. | Technical protection should be combined with authorization and accountability controls. |
| Role of logging | Logging is secondary to active monitoring and enforcement. | Logging is the central mechanism for preserving evidence and detecting tampering. | Records and audit trails support compliance, review, and investigation. | Logs should be protected, retained, and correlated with application records. |
| Role of tracing | SaBRe supports efficient system-call tracing and controlled program instrumentation. | Live tracing reconstructs system behavior for forensic analysis. | Tracing is not the primary focus but could strengthen investigations of CDS failures. | Tracing can connect a high-level CDS failure to specific OS operations. |
| Data-integrity contribution | Protects kernel state and process privileges that could otherwise enable data manipulation. | Helps demonstrate whether records were altered and reconstruct the sequence of events. | Establishes expectations for complete, accurate, attributable, and reliable pharmaceutical data. | Data integrity requires prevention, evidence preservation, and validated processes. |
| Performance considerations | SaBRe generally reports low overhead, while AKO introduces monitoring within the kernel. | Continuous logging and tracing may require storage, processing, and retention management. | Validation must demonstrate that controls do not compromise laboratory performance or data acquisition. | CDS implementations must balance monitoring depth with real-time acquisition needs. |
| Applicability to CDS environments | Protects acquisition processes, drivers, and privileged operations but requires CDS validation. | Useful for investigating acquisition failures, file changes, and system-level incidents. | Directly relevant to regulated CDS governance, validation, and laboratory data management. | The strongest approach integrates OS controls with CDS audit trails and quality procedures. |
| Main limitation | Demonstrated mainly in Linux environments and may not directly apply to Windows-based CDS platforms. | Requires reliable time synchronization, protected storage, suitable configuration, and specialist analysis. | May provide limited technical detail about kernel events, system calls, or OS-level attacks. | A gap remains between low-level OS research and practical pharmaceutical CDS implementation. |
| Future research direction | Adapt mechanisms for Windows and validated CDS architectures. | Integrate logs and traces with instrument, application, database, and audit records. | Develop risk-based validation models that explicitly include OS logging, tracing, and access control. | Future work should evaluate combined technical and procedural controls in real CDS environments. |
| Overall contribution | Provides active prevention and execution-level control. | Provides detection, reconstruction, and tamper evidence. | Provides governance, validation, and regulatory assurance. | The papers support a layered model for protecting chromatographic data integrity. |
##Overall Analysis
The reviewed papers can be grouped into three areas:OS-Level Protection and Rewriting,Logging, Tracing, and Tamper Evidence,and Pharmaceutical Data-Integrity Controls.
SaBRe[10] and AKO[16] focus on active operating-system and process-level protection, particularly system-call behavior and privilege changes. 
SealFSv2[11] and live system-call trace reconstruction focus on preserving evidence, detecting tampering, and understanding system activity after or during an event. 
The pharmaceutical studies focus on validation, quality systems, and the organizational controls needed to ensure that computerized laboratory systems produce reliable data [12].
A major research gap is the limited integration between these technical mechanisms and chromatography data systems. 
Most OS-level techniques are demonstrated in Linux or general-purpose computing environments, whereas CDS platforms commonly operate on Windows and require validated, stable, and highly controlled configurations.
Future research should therefore investigate how kernel monitoring, protected logging, tracing, file-integrity controls, and risk-based validation can be combined in real CDS environments without disrupting instrument communication or data acquisition.

## 6. Gaps, Limitations and Future Directions
Although the paper discussed has explained operating systems and the events, they have not sufficiently established the direct relationship between the operating-system layer and the applications used in chromatography data systems (CDSs). 
Although Linux-based systems generally support a broader range of operations and configuration options than Windows, Windows remains the most widely used platform in CDS environments. 
This highlights the need for further research focusing specifically on Windows-based CDS architectures, including their security requirements and data-integrity controls.
Another limitation is that cybersecurity discussions often emphasize external attacks and remote intrusions. 
In practice, common risks in CDS environments are associated with privilege escalation and the intentional or unintentional manipulation of data. 
Future research should therefore examine internal controls, privilege management, user and process monitoring, and the integration of operating-system logs with application and instrument records. 
Such an approach could improve the detection and traceability of unauthorized changes while strengthening data integrity and regulatory compliance.
## 7. Conclusion
This literature review demonstrates that data integrity in chromatography data systems depends not only on the CDS application and analytical instruments, but also on the operating system that supports their operation.
OS-level events, including kernel activity, authentication, process and service changes, file-system operations, and device communications, can provide valuable evidence about the conditions affecting data acquisition, processing, and storage.
Logging, tracing, access control, and observability offer complementary forms of protection. 
Access-control and kernel-level mechanisms can prevent unauthorized privilege changes, while logs and traces support the detection, reconstruction, and investigation of system activity. 
Tamper-evident logging further strengthens the reliability of recorded evidence. 
However, these technical mechanisms must be implemented within validated computerized systems and integrated with application audit trails, instrument records, quality procedures, and regulatory controls.
The reviewed literature also reveals a significant gap between operating-system security research and practical chromatography data-system environments. 
Many proposed techniques are demonstrated in Linux or general-purpose systems, whereas CDS platforms commonly rely on Windows, specialized drivers, and highly controlled configurations. 
Future research should therefore evaluate OS-level logging, tracing, access control, file-integrity monitoring, and risk-based validation in real CDS environments. 
Such work should consider performance, compatibility, regulatory compliance, and the prevention of both intentional and accidental data manipulation. 
Overall, a layered approach combining prevention, monitoring, evidence preservation, and governance provides the strongest foundation for maintaining trustworthy chromatographic data.

## 8. References
[1]: Aris Koumandaros, The Prevention of Data Integrity Failures in Pharmaceutical Manufacturing Through Risk-Based Validation of Computerized Systems, Faculty of California State University, Dominguez Hills, 2021.
[2]: Freek Varossieau, Data integrity in CDS, Agilent, 2018
[3]: WHO TRS 1033, Annex 4, Guideline on data integrity, 2021.
[4]: Pamela Campbell, IT in Pharma Countering the Information Security Risk, pharma Focus Asia, 2020
[5]: PIC/S PI 09-18 Annex 11 Computerized System Validation, 09-2026.
[6]: 21 CFR PART 11 Electronic Records & Electronic Signature, 04/2026
[7]: K.Stouffer, M.Pease, C.Tang and others, Guide to Operational Technology (OT) Security, NIST, 2026
[8]: Hamza Megahed, Engineering Everything with eBPF, https://github.com/Hamza-Megahed/Engineering-Everything-with-eBPF-Code 
[9]: Hiroki Kuzuno & Toshihiro Yamauchi, Mitigation of privilege escalation attack using kernel data relocation mechanism, International Journal of Information Security, 2024.
[10]: P. Arras, A. Andronidis, L. Pina, K. Mituzas, Q. Shu, D.Grumberg, C. Cadar, SaBRe: load-time selective binary rewriting, International Journal on Software Tools for Technology Transfer, 2022 , DOI: 10.1007/s10009-021-00644-w
[11]: Gorka Guardiola-Múzquiz & Enrique Soriano-Salvador, SealFSv2: combining storage-based and ratcheting for tamper-evident logging International Journal of Information Security, 2023 DOI: 10.1007/s10207-022-00643-1
[12]: Thanh Nguyen, Meni Orenbach, Ahmad Atamli, Live system call trace reconstruction on Linux Forensic Science International: Digital Investigation, 2022. DOI: 10.1016/j.fsidi.2022.301398
[13]: Patel Richi & Rajgor Hiral A. Data Integrity in Pharmaceutical Quality System, International Journal of Pharmaceutical Research and Development, 2025 DOI: 10.33545/26646862.2025.v7.i2j.253
[14]: Silberschatz, A., Galvin, P. B., & Gagne, G. Operating System Concepts. Wiley, 2018
[15]: Integrated Laboratory Informatics Systems Deliver Greater Efficiency and Improved Data Integrity
[16]: T.Yamauchi. Y.Akao, R.Yashitani, Additional kernel observer: privilege escalation attack prevention mechanism focusing on system call privilege changes International Journal of Information Security, 2021 DOI: 10.1007/s10207-020-00514-7
[17]: إباء عويشق، مقدمة في نظم التشغيل، الجامعة الافتراضية السورية،2018
[18]: غيث مصطفى، مقرر نظم التشغيل، الجامعة الافتراضية السورية، 2026 

## 9. Process Evidence
### 9.1 Search Log Summary
Google Scholar, IEEE Xplore, ScienceDirect, ACM Digital Library, NIST, WHO, FDA, and PIC/S official websites.
**Key search strings:**
"operating systems" AND logging
"operating systems" AND tracing
"system calls" AND security
"Linux kernel" AND data integrity
"file systems" AND tamper-evident logging
"Chromatography Data Systems" AND access control
"CDS" AND data acquisition
"CDS" AND audit trails
"data integrity" AND ALCOA+
"data integrity" AND privilege management
"data integrity" AND risk-based validation
"pharmaceutical data integrity" AND GMP compliance
"electronic records" AND system validation
"operational technology security" AND pharmaceutical manufacturing
Filters applied: publication date, academic credibility, relevance to operating systems/ data integrity/ CDS, and availability of full-text information
### 9.2 Annotated Bibliography (minimum 6 sources)
**Source 1**
Citation: Aris Koumandaros, The Prevention of Data Integrity Failures in Pharmaceutical Manufacturing Through Risk-Based Validation of Computerized Systems, Faculty of California State University, Dominguez Hills, 2021.
Annotation: 
Summary: This study examines how risk-based validation of computerized systems can prevent data-integrity failures in pharmaceutical manufacturing.
Relevance: It is directly relevant because it connects computer-system validation with the accuracy, reliability, and security of pharmaceutical data. It also explains how identifying risks can improve compliance and reduce errors in regulated environments.
Limitation: As an academic thesis, its conclusions may focus mainly on pharmaceutical manufacturing and may not apply equally to other industries or operating-system environments.
**Source 2**
Citation: Freek Varossieau, Data integrity in CDS, Agilent, 2018
Annotation: 
Summary:Practical guide to all issues related to data integrity in CDS, describe how Agilent application complies with pharmaceutical guidelines,, including the importance of accurate data collection, storage, processing, and reporting.
Relevance: It is relevant to the research because CDS platforms depend on computerized systems and operating-system controls to protect laboratory data. The source helps explain how access control, audit trails, and reliable system configuration support trustworthy scientific results.
Limitation: The source is published by Agilent, a commercial organization, so it may emphasize the company’s products or perspective and may not provide the same level of independence as a peer-reviewed academic article.
**Source 3**
Citation: WHO TRS 1033, Annex 4, Guideline on data integrity, 2021.
Annotation: 
Summary: This guideline presents principles and recommendations for maintaining data integrity in pharmaceutical and healthcare-related environments. It addresses data governance, documentation, audit trails, access control, and reliable records.
Relevance: The source is highly relevant because it provides internationally recognized guidance for ensuring that data remains complete, consistent, accurate, and traceable throughout its life cycle. It also supports the discussion of regulatory expectations for computerized systems.
Limitation:It contains what to do, not how to do it, It does not provide detailed technical explanations of how operating-system mechanisms implement every security or integrity control
**Source 4**
Citation: Pamela Campbell, IT in Pharma Countering the Information Security Risk, pharma Focus Asia, 2020.
Annotation: 
Summary: This article discusses information-security risks in the pharmaceutical industry and presents approaches for protecting systems, data, and business operations.
Relevance: It is relevant because pharmaceutical organizations rely heavily on information technology, computerized laboratory systems, and electronic records. The article helps connect operating-system security concepts, such as access management and monitoring, with practical cybersecurity risks in pharmaceutical companies.
Limitation: As an industry publication, the article may provide a practical overview rather than detailed academic analysis. Some recommendations may also become outdated as cyber threats and security technologies continue to evolve.
**Source 5**
Citation: PIC/S PI 09-18 Annex 11 Computerized System Validation, 09-2026.
Annotation: 
Summary: This document provides guidance on validating computerized systems used in regulated pharmaceutical environments. It emphasizes risk management, system documentation, testing, security controls, change management, and maintaining data integrity.
Relevance: It is relevant because validation ensures that computerized systems perform consistently and produce reliable records. The guidance also demonstrates how operating-system functions, user permissions, backups, and audit trails support compliance and trustworthy data.
Limitation: The document is designed mainly for pharmaceutical regulatory environments. Therefore, its requirements may be too specialized for general operating-system applications or organizations outside the life-sciences sector.
**Source 6**
Citation: 21 CFR PART 11 Electronic Records & Electronic Signature, 04/2026
Annotation: 
Summary: This regulation establishes requirements for electronic records and electronic signatures used by organizations regulated by the U.S. Food and Drug Administration. It covers system controls, authentication, audit trails, record protection, and electronic-signature management.
Relevance: It is important because it explains the legal and technical controls required to ensure that electronic records are trustworthy and cannot be changed without detection. These requirements are closely connected to operating-system security, identity management, and access control.
Limitation: The regulation applies specifically to FDA-regulated organizations in the United States. It may not fully address international requirements or provide detailed implementation instructions for particular operating systems.
**Source 7**
Citation: K.Stouffer, M.Pease, C.Tang and others, Guide to Operational Technology (OT) Security, NIST, 2026
Annotation: 
Summary: This guide explains security principles and practices for protecting operational-technology environments. It discusses system architecture, risk management, monitoring, access control, incident response, and the differences between IT and OT security.
Relevance: The source is relevant because many pharmaceutical manufacturing systems combine computerized information systems with operational technology. It helps explain how security controls can protect the availability, integrity, and safety of industrial processes.
Limitation: The guide focuses on OT environments and may not provide detailed information about pharmaceutical data-integrity requirements or traditional desktop and server operating systems.
**Source 8**
Citation:Hamza Megahed, Engineering Everything with eBPF. 
Annotation: 
Summary: This project presents examples and code related to eBPF, a Linux technology that allows programs to observe and interact with system and kernel events. It demonstrates how eBPF can be used for monitoring, tracing, networking, and security.
Relevance: It is relevant because eBPF provides practical mechanisms for observing operating-system behavior without modifying the kernel directly. This capability can support security monitoring, system auditing, performance analysis, and detection of suspicious activity.
Limitation: The project is hosted on GitHub and may not have undergone formal peer review. Its quality and completeness may depend on the author’s implementation, documentation, and future maintenance.
**Source 9**
Citation:Hiroki Kuzuno & Toshihiro Yamauchi, Mitigation of privilege escalation attack using kernel data relocation mechanism, International Journal of Information Security, 2024 
Annotation: 
Summary: This article investigates a kernel-data relocation mechanism designed to reduce the risk of privilege-escalation attacks. It focuses on protecting sensitive kernel information and making exploitation more difficult.
Relevance: The source is relevant because privilege escalation is a major operating-system security threat. Protecting kernel data can prevent attackers from gaining unauthorized access or increasing their system privileges. The article also demonstrates how low-level kernel mechanisms contribute to system integrity.
Limitation: The proposed technique may require specific kernel support and could introduce performance or compatibility concerns. Its effectiveness may also depend on the attack methods and system configurations evaluated by the researchers.
**Source 10**
Citation: P. Arras, A. Andronidis, L. Pina, K. Mituzas, Q. Shu, D.Grumberg, C. Cadar, SaBRe: load-time selective binary rewriting, International Journal on Software Tools for Technology Transfer, 2022
Annotation: 
Summary: This article presents SaBRe, a system for selectively rewriting binary programs when they are loaded. The technique can modify selected program behavior without requiring access to the original source code.
Relevance: It is relevant to operating systems because load-time binary rewriting can support program analysis, security monitoring, debugging, and vulnerability mitigation. It demonstrates how software can be instrumented at a low level while remaining compatible with existing applications.
Limitation: Binary rewriting may create performance overhead, compatibility problems, or difficulties when dealing with complex software. The technique may also be challenging to deploy safely in highly regulated production environments.
**Source 11**
Citation: Gorka Guardiola-Múzquiz & Enrique Soriano-Salvador, SealFSv2: combining storage-based and ratcheting for tamper-evident logging International Journal of Information Security, 2023
Annotation: 
Summary: This article introduces SealFSv2, a logging approach that combines storage-based protection and ratcheting mechanisms to make unauthorized changes to logs detectable.
Relevance: It is highly relevant to data integrity and operating-system security because reliable logs are essential for auditing, incident investigation, and proving that system events have not been altered. The approach may help protect security records from tampering by attackers.
Limitation: Tamper-evident logging can require additional storage, processing, and management resources. The technique detects unauthorized modification but may not prevent the original attack or guarantee the recovery of deleted data.
**Source 12**
Citation:Thanh Nguyen, Meni Orenbach, Ahmad Atamli, Live system call trace reconstruction on Linux Forensic Science International: Digital Investigation, 2022 
Annotation: 
Summary: This article presents a method for reconstructing system-call activity on live Linux systems. System calls provide important evidence about how programs interact with the kernel and system resources.
Relevance: The source is relevant because system-call tracing can support digital forensics, security monitoring, intrusion investigation, and analysis of suspicious operating-system behavior. It also shows how kernel-level information can help reconstruct events after a security incident.
Limitation: The method is focused on Linux and may not work in exactly the same way on Windows or other operating systems. Live forensic analysis can also affect system performance and may produce incomplete evidence in some situations.
**Source 13**
Citation: Patel Richi & Rajgor Hiral A. Data Integrity in Pharmaceutical Quality System, International Journal of Pharmaceutical Research and Development, 2025
Annotation: 
Summary: This article discusses the importance of data integrity within pharmaceutical quality systems. It examines principles such as accurate documentation, traceability, secure records, and compliance with regulatory expectations.
Relevance: It is relevant because pharmaceutical quality depends on trustworthy electronic and paper-based data. The article supports the argument that computerized systems must protect information from unauthorized changes, loss, or incorrect processing.
Limitation: The article may focus more on quality-management principles than on the technical details of operating systems and cybersecurity controls. Its recommendations may also require adaptation for different regulatory jurisdictions.
**Source 14**
Citation: Silberschatz, A., Galvin, P. B., & Gagne, G. Operating System Concepts. Wiley, 2018
Annotation: 
Summary: This textbook explains the fundamental concepts of operating systems, including processes, memory management, storage, file systems, security, and system protection.
Relevance: It is one of the most useful foundational sources for this research because it provides the theoretical background needed to understand how operating systems manage resources and protect data. The book also helps explain the role of kernels, system calls, authentication, and access control.
Limitation: Since it was published in 2018, some technologies and security threats may not reflect the latest developments. It also provides general operating-system knowledge rather than specialized pharmaceutical-compliance guidance.
**Source 15**
Citation: Integrated Laboratory Informatics Systems Deliver Greater Efficiency and Improved Data Integrity
Annotation: 
Summary: This source discusses how integrated laboratory informatics systems can improve laboratory efficiency and strengthen data integrity. It likely focuses on connecting laboratory processes, information management, and electronic records.
Relevance: It is relevant because integrated systems can reduce manual data entry, improve traceability, and make laboratory information easier to monitor and control. These benefits are important in pharmaceutical environments where reliable data is necessary for quality and regulatory compliance.
Limitation: The citation does not include an author, publication date, publisher, or URL. Therefore, it is difficult to evaluate the source’s credibility, verify its claims, or provide a complete academic reference.
**Source 16**
Citation: T.Yamauchi. Y.Akao, R.Yashitani, Additional kernel observer: privilege escalation attack prevention mechanism focusing on system call privilege changes International Journal of Information Security, 2021
Annotation: 
Summary: This article proposes an additional kernel observer that focuses on changes in system-call privileges to prevent privilege-escalation attacks. It monitors security-sensitive behavior at the kernel level.
Relevance: The source is relevant because system calls are a central interface between applications and the operating system. Monitoring changes in their privileges can help detect abnormal behavior and prevent unauthorized access to protected resources.
Limitation: Kernel-level monitoring may introduce performance overhead and implementation complexity. The mechanism may also require modifications or additional components that are difficult to deploy in existing systems.
**Source 17**
Citation:إباء عويشق، مقدمة في نظم التشغيل، الجامعة الافتراضية السورية،2018 
Annotation: 
Summary: This textbook provides an introduction to operating-system concepts, including processes, memory, files, storage, and system management. It is written for students who are beginning to study operating systems.
Relevance: The source is relevant because it provides basic explanations in Arabic and supports understanding of the fundamental concepts discussed in the research. It can also help connect theoretical course material with the technical topics addressed by English-language sources.
Limitation: The book may provide an introductory rather than advanced treatment of security, data integrity, and modern kernel technologies. In addition, some information may require updating as operating systems and cybersecurity methods develop.
**Source 18**
Citation: غيث مصطفى، مقرر نظم التشغيل، الجامعة الافتراضية السورية، 2026
Annotation: 
Summary: This course material presents the main concepts of operating systems and explains topics related to process management, memory, storage, files, and system operation.
Relevance: It is relevant because it represents the official course content and provides the academic foundation for the research. It helps the group connect the selected articles and practical applications with the concepts studied in the Operating Systems course.
Limitation: As course material, it may focus on teaching the required syllabus rather than providing detailed research findings or recent experimental results. It may also contain fewer practical examples than specialized technical and academic publications.
### 9.3 Group Reflection (300–400 words)
The hardest part for our group was preparing the comparison and analysis table. 
We had to identify the main ideas from different sources and compare them according to their methods, results, advantages, and limitations. 
Organizing this information clearly was challenging because each article used different terminology and focused on different aspects of the operating-system topic.
However, completing the table helped us understand the similarities and differences between the sources and supported our final analysis.
Another important skill we learned was how to use suitable keywords and academic databases to find reliable articles.
At the beginning, searching for relevant literature was difficult because general search terms produced too many unrelated results. 
By using more specific keywords and applying filters, we were able to find better sources through academic databases. 
We also learned how to evaluate the credibility and relevance of each article before including it in our research.
Applying academic concepts changed our understanding of the topic from theoretical to practical.
Previously, we understood operating-system concepts mainly as definitions from textbooks or lectures. 
Through this project, we discovered how these concepts are applied in real systems and how they influence computer performance, resource management, security, and user experience.
Comparing different studies helped us connect classroom knowledge with practical situations.
One of the greatest challenges we faced was writing in English. Expressing technical ideas accurately and using appropriate academic vocabulary required considerable effort. 
We also struggled to summarize literature that consisted of many pages into only a few clear lines. 
This process taught us how to identify the main argument, important evidence, and useful conclusions without copying unnecessary details.
Although the project required substantial cooperation and revision, it improved our research, communication, critical-thinking, and academic-writing skills.
We learned that successful research requires more than collecting information; it also requires analyzing, comparing, summarizing, and presenting evidence logically. 
Overall, this experience deepened our understanding of operating systems and showed us the value of applying academic knowledge to practical computer-science problems.
## 10. AI Use Disclosure
We used AI to identify the most important ideas in the course and the topics related to it in real-life applications.
We also used it to formulate the comparison, rephrase some statements in correct English, explain certain assignment requirements, and guide us on how to write using Markdown.
