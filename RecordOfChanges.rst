


Record of Changes
=================

Overview of changes in documentation from previous editions.

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
     - :doc:`/AdminManual/Appendixes/CSParams/index`
     - Added more email templates
   * - **2.30**
     -
     - :doc:`/Concepts/ContactMerger`
     - Added contact merger concept, tasks and email template
   * -
     -
     - :doc:`/AdminManual/Appendixes/CSParams/index`
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
     - :doc:`/ReleaseNotes/Upgrade-2-35-howto`
     - An ad-hoc guide to database upgrade specifics in this release
   * -
     -
     - :doc:`System requirements </AdminManual/Installation/SystemReqs>`
     - Increased minimum version of PostgreSQL
   * -
     -
     - :doc:`Customization </AdminManual/Customization>`,
       :doc:`CSParams </AdminManual/Appendixes/CSParams/index>`
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
     - Extracted to a separate publication
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
