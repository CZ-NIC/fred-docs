

Status mapping
---------------

.. Note:: This reference lists external status flags only.

   The RDAP server contains the mapping of **all** status flags as specified
   in :rfc:`8056#section-2`. Not all of them, however, are employed in the FRED
   backend, because FRED has a customized set of status flags.

.. list-table:: FRED EPP-to-RDAP Status Mapping
   :widths: 20 40 40
   :header-rows: 1

   * - Std/FRED [#]_
     - Status flag
     - RDAP status
   * - FRED
     - contactPassedManualVerification
     - validated
   * - FRED
     - deleteCandidate
     - pending delete
   * - Std
     - linked
     - associated
   * - FRED
     - outzone
     - inactive
   * - Std
     - serverDeleteProhibited
     - server delete prohibited
   * - Std
     - serverRenewProhibited
     - server renew prohibited
   * - Std
     - serverTransferProhibited
     - server transfer prohibited
   * - Std
     - serverUpdateProhibited
     - server update prohibited
   * - FRED
     - validatedContact
     - validated

.. [#] Indication whether the status flag is FRED custom (``FRED``)
   or EPP standard (``Std``).
