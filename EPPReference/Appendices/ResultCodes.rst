


Result codes & messages
=======================

.. https://admin.nic.cz/wiki/developers/fred/EPP/backend/spec#GetErrorMessage

.. list-table:: Successful command completion responses
   :header-rows: 1
   :widths: 10, 30, 60

   * - Code
     - Message
     - Description
   * - 1000
     - Command completed successfully
     - desc
   * - 1001
     - Command completed successfully; action pending
     - desc
   * - 1300
     - Command completed successfully; no messages
     - desc
   * - 1301
     - Command completed successfully; ack to dequeue
     - desc
   * - 1500
     - Command completed successfully; ending session
     - desc

.. list-table:: Command error responses
   :header-rows: 1
   :widths: 10, 30, 60

   * - Code
     - Message
     - Description
   * - 2000
     - Unknown command
     - desc
   * - 2001
     - Command syntax error
     - desc
   * - 2002
     - Command use error
     - desc
   * - 2003
     - Required parameter missing
     - desc
   * - 2004
     - Parameter value range error
     - desc
   * - 2005
     - Parameter value syntax error
     - desc
   * - 2100
     - Unimplemented protocol version
     - desc
   * - 2101
     - Unimplemented command
     - desc
   * - 2102
     - Unimplemented option
     - desc
   * - 2103
     - Unimplemented extension
     - desc
   * - 2104
     - Billing failure
     - desc
   * - 2105
     - Object is not eligible for renewal
     - desc
   * - 2106
     - Object is not eligible for transfer
     - desc
   * - 2200
     - Authentication error
     - desc
   * - 2201
     - Authorization error
     - desc
   * - 2202
     - Invalid authorization information
     - desc
   * - 2300
     - Object pending transfer
     - desc
   * - 2301
     - Object not pending transfer
     - desc
   * - 2302
     - Object exists
     - desc
   * - 2303
     - Object does not exist
     - desc
   * - 2304
     - Object status prohibits operation
     - desc
   * - 2305
     - Object association prohibits operation
     - desc
   * - 2306
     - Parameter value policy error
     - desc
   * - 2307
     - Unimplemented object service
     - desc
   * - 2308
     - Data management policy violation
     - desc
   * - 2400
     - Command failed
     - desc
   * - 2500
     - Command failed; server closing connection
     - desc
   * - 2501
     - Authentication error; server closing connection
     - desc
   * - 2502
     - Session limit exceeded; server closing connection
     - desc
