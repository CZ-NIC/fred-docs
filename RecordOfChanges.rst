


Record of Changes
=================

Overview of changes in documentation from previous editions.
For changes in software, see :doc:`/ReleaseNotes/index`.

The newest are :ref:`at the end <roc-end>`.

.. tabularcolumns:: |p{0.075\textwidth}|p{0.075\textwidth}|p{0.25\textwidth}|p{0.575\textwidth}|

.. list-table::
   :header-rows: 1
   :widths: 8, 8, 26, 58

   * - Version
     - Edition
     - Segment
     - Change description
   * - older
     -
     - :doc:`/AdminManual/Appendixes/EmailParameters`
     - Added more email templates
   * - **2.30**
     -
     - :doc:`/Concepts/ContactMerger`
     - Added contact merger concept, tasks and email template
   * -
     -
     - :doc:`/AdminManual/Appendixes/EmailParameters`
     - Added a new CS parameter
   * - **2.31**
     -
     - :doc:`/Concepts/AKM`
     - Added :term:`AKM` concept, components, task and email templates
   * - **2.32**
     -
     - :ref:`config-handles`
     - Added configurable handle format validation
   * -
     -
     - :ref:`config-dn`
     - Added configurable domain name format validation
   * - **2.33**
     - **1.0**
     - :doc:`/EPPReference/index`
     - Added mailing address extension of contacts
   * -
     -
     - :doc:`/EPPReference/Appendixes/ErrorReasons`
     - New texts of EPP error reasons
   * -
     - **1.1**
     - :doc:`/Features/General/index`
     - Added record statements feature, component and email template
   * -
     - **1.2**
     - :doc:`/EPPReference/ManagedObjects/index`
     - Added divergence from the standards of object mapping in FRED EPP
   * -
     -
     - :doc:`/Concepts/Teccheck`
     - Expanded on the concept of technical checks
   * - **2.34**
     - **1.0**
     - :doc:`/ReleaseNotes/index`
     - Added release notes
   * -
     -
     - :doc:`Diagram of FRED components </Architecture/TopLevelComponents/index>`
     - Removed dependency on ``fred-logd`` from ``fred-pifd``
   * -
     -
     - :ref:`cronjob-regular` and :ref:`cronjob-object-deletion`
     - Procedures accept object types by name, new argument, removed dependency on ``fred-rifd``
   * -
     - **1.1**
     - :doc:`/Concepts/ContactMerger` and :ref:`contact-merge`
     - Criteria of destination contact selection in an automatic merger, some minor rephrasing
   * -
     -
     - :doc:`/EPPReference/CommandStructure/Update/UpdateDomain`
     - Mention of nsset and keyset unlinking with empty elements
   * - **2.35**
     - **1.0**
     - :doc:`/ReleaseNotes/index`
     - Added release notes for FRED 2.35
   * -
     -
     - :doc:`/ReleaseNotes/Upgrade-2-35`
     - An ad-hoc guide to database upgrade specifics in this release
   * -
     -
     - :doc:`System requirements </AdminManual/Installation/SystemReqs>`
     - Increased minimum version of PostgreSQL
   * -
     -
     - :doc:`Customization </AdminManual/Customization/Email>`,
       :doc:`Email Params </AdminManual/Appendixes/EmailParameters>`
     - Changed email template database table name
   * -
     -
     - :doc:`Features </Features/General/RecordStatements>`,
       :doc:`Features </Features/AdminIF/WebAdmin>`,
       :doc:`Components </Architecture/TopLevelComponents/index>`,
       :ref:`Components <FRED-Arch-servers-rsif>`,
       :ref:`Task <generate-rs>`
     - Generation of historical record statements in Daphne
   * -
     -
     - :doc:`Features admin </Features/AdminIF/CLIAdmin>`
     - New administration feature to manage objects
   * -
     -
     - :doc:`Source code </Architecture/SourceCode>`
     - Added list of GitHub repositories
   * -
     -
     - :ref:`ORB parameters <config-servers-omni>`
     - Added minimum omniORB settings for FRED servers
   * - **2.36**
     - **1.0**
     - :doc:`/ReleaseNotes/index`
     - Added release notes for FRED 2.36
   * -
     -
     - :doc:`/Concepts/index`
     - Extracted to a separate publication
   * -
     -
     - :doc:`/Concepts/LifeCycle/index`
     - Added object life cycle
   * -
     -
     - :doc:`/Concepts/Contacts`
     - Added contacts
   * -
     - **1.1**
     - :doc:`/AdminManual/Installation/SourceTar`
     - Upgraded installation procedure to use source from GitHub,
       new signing key for secure apt
   * -
     - **1.2**
     - :doc:`/ReleaseNotes/index`
     - Added release notes for the version 2.36.1; upgraded to a newer Sphinx
   * - **2.37**
     - **1.0**
     - :doc:`/ReleaseNotes/index`
     - Added release notes for FRED 2.37.0
   * -
     -
     - :doc:`/Features/General/index`
     - Added GDPR compliance as a new FRED feature
   * -
     -
     - :doc:`/EPPReference/PoliciesRules`
     - Added a new chapter
   * -
     -
     - :doc:`/EPPReference/CommandStructure/Create/CreateContact`,
       :doc:`/EPPReference/CommandStructure/Update/UpdateContact`,
       :doc:`/EPPReference/CommandStructure/Info/InfoContact`
     - Improved explanations about information disclosure
   * -
     -
     - :ref:`epp-poll-type-update`
     - Added a poll-message type about contact update
   * -
     -
     - :doc:`/AdminManual/AdministrativeTasks/Objects`
     - Added a new public-request type
   * -
     -
     - :ref:`cronjob-public-requests`
     - Added a cronjob to process public requests for personal information
   * -
     -
     - :doc:`/AdminManual/Appendixes/EmailParameters`
     - Added a new email template for sending personal information
   * -
     - **1.1**
     - :doc:`/ReleaseNotes/index`
     - Added release notes for the version 2.37.1
   * -
     -
     - :doc:`/ReleaseNotes/Upgrade-2-37`
     - Added considerations before upgrading
   * -
     -
     - :doc:`/Concepts/ContactMerger`
     - Corrected the definition of identical contacts
   * -
     -
     - :ref:`cronjob-contact-merger`
     - Added a cronjob
   * -
     - **1.2**
     - :doc:`/AdminManual/Installation/SystemReqs`
     - Discontinued support for Ubuntu 14
   * -
     -
     - :doc:`/AdminManual/Installation/BinsUbuntu`
     - Updated the installation script and its description
   * -
     - **1.3**
     - :ref:`config-contact-reminder`
     - Added a configurable database table
   * -
     -
     - :doc:`/Concepts/Billing`
     - Added a very general description of handling money in the FRED
   * -
     -
     - :doc:`/AdminManual/Appendixes/EmailParameters`
     - Reviewed mail template parameters
   * -
     - **1.4**
     - :doc:`/Concepts/EPPClientWorkflow`
     - Added a description of a general EPP client workflow
   * -
     -
     - :doc:`/RDAPReference/index`
     - Added an RDAP reference guide
   * -
     - **1.5**
     - :doc:`/Concepts/UsersInterfaces`
     - Added an introduction to FRED's users and user interfaces
   * -
     -
     - :doc:`/Concepts/Communication`
     - Added an overview of FRED's communication (notifications, warnings, etc.)
   * -
     -
     - :doc:`/Features/PublicIF/index`
     - Added a list of Public interface features
   * -
     - **1.6**
     - :ref:`Audit log feature <features-gen-auditlog>`,
       :doc:`Audit log concept </Concepts/AuditLog>`
     - Added the audit log
   * -
     -
     - :doc:`/Architecture/Deployment`
     - Added an example of distributed deployment
   * - **2.38**
     - **1.0**
     - :doc:`/ReleaseNotes/index`
     - Added release notes for FRED 2.38.0, 2.37.3 and 2.37.2
   * -
     -
     - :doc:`/ReleaseNotes/Upgrade-2-38`
     - Added considerations before upgrade
   * -
     -
     - :ref:`features-gen-billing`, |br|
       :doc:`/Concepts/Billing`, |br|
       :doc:`/Concepts/PAIN`, |br|
       :doc:`/Architecture/BlackboxModel`, |br|
       :doc:`/Architecture/TopLevelComponents/index`, |br|
       :doc:`/AdminManual/Configuration`, |br|
       :ref:`cron-collect-payments`, |br|
       :ref:`daphne-task-assign-payment`
     - Added or changed according to PAIN Phase 1
       (see :doc:`the release notes </ReleaseNotes/index>`)
   * -
     -
     - :ref:`contact-disclosure`,
       :ref:`config-contact-disclosure`,
       :doc:`/EPPReference/PoliciesRules`
     - Changed disclosure policies to configurable
   * -
     -
     - :ref:`install-dist`
     - Marked more packages as ported to setuptools
   * -
     -
     - :ref:`FRED-Admin-reginit-zone-ns`
     - Changed syntax of the command
   * -
     -
     - :ref:`resolve-public-request`
     - Changed the name of the status of new public requests
   * -
     -
     - :ref:`config-dbparams`
     - Revised configuration of basic :term:`db` parameters
   * -
     -
     - /AdminManual/Extensions,
       :doc:`/Architecture/TopLevelComponents/CORBAClients`
     - Removed :term:`CZ-specific` front-end extensions,
       because they are not released to the public
   * -
     -
     - :doc:`/AdminManual/Installation/BinsUbuntu`
     - Revised the installation process a tiny bit
   * -
     - **1.1**
     - :doc:`/ReleaseNotes/index`
     - Corrected the note in 2.38.0 about the ``sendauthinfo`` bugfix
   * -
     - **1.2**
     - :doc:`/ReleaseNotes/index`
     - Added release notes for FRED 2.38.1
   * -
     - **1.3**
     - :ref:`system-reqs`
     - Updated supported Fedora versions
   * -
     -
     - :doc:`/AdminManual/Installation/BinsUbuntu`,
       :doc:`/AdminManual/Installation/BinsFedora`
     - Updated installation procedures
   * -
     - **1.4**
     - :doc:`/ReleaseNotes/index`
     - Added release notes for FRED 2.38.{2,3,4,5} and FRED 2.39.0
   * - **2.39**
     - **1.0**
     - :doc:`/Architecture/SourceCode`
     - Added libfred component and updated build groups
   * -
     -
     - :doc:`/AdminManual/Installation/SourceTar`
     - Updated installation procedure with new tools
   * -
     -
     - :doc:`/AdminManual/AdministrativeTasks/Objects`
     - Contact unblocking together with domain now possible
   * -
     -
     - :doc:`/AdminManual/Customization/index`
     - Customization reworked for email templates and state-change notifications
   * -
     - **1.1**
     - :doc:`/AdminManual/Customization/Web`
     - Added webwhois customization and template reference

       .. _roc-end:
   * -
     - **1.2**
     - :doc:`/AdminManual/Installation/BinsUbuntu`,
       :doc:`/AdminManual/Installation/BinsFedora`
     - Updated installation procedures - system registrar required for servers to launch
