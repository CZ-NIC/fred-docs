


Result codes & messages
=======================

The result codes and messages are taken from the :rfc:`5730#section-3`
where they are described in detail.

The result messages are provided in the language of :doc:`the session
</EPPReference/CommandStructure/Login>`.

Successful command completion responses
---------------------------------------

.. list-table::
   :header-rows: 1
   :widths: 30, 70

   * - Code
     - Message
   * - 1000
     - Command completed successfully
   * - 1001
     - Command completed successfully; action pending
   * - 1300
     - Command completed successfully; no messages
   * - 1301
     - Command completed successfully; ack to dequeue
   * - 1500
     - Command completed successfully; ending session


Command error responses
-----------------------

.. list-table::
   :header-rows: 1
   :widths: 30, 70

   * - Code
     - Message
   * - 2000
     - Unknown command
   * - 2001
     - Command syntax error
   * - 2002
     - Command use error
   * - 2003
     - Required parameter missing
   * - 2004
     - Parameter value range error
   * - 2005
     - Parameter value syntax error
   * - 2100
     - Unimplemented protocol version
   * - 2101
     - Unimplemented command
   * - 2102
     - Unimplemented option
   * - 2103
     - Unimplemented extension
   * - 2104
     - Billing failure
   * - 2105
     - Object is not eligible for renewal
   * - 2106
     - Object is not eligible for transfer
   * - 2200
     - Authentication error
   * - 2201
     - Authorization error
   * - 2202
     - Invalid authorization information
   * - 2300
     - Object pending transfer
   * - 2301
     - Object not pending transfer
   * - 2302
     - Object exists
   * - 2303
     - Object does not exist
   * - 2304
     - Object status prohibits operation
   * - 2305
     - Object association prohibits operation
   * - 2306
     - Parameter value policy error
   * - 2307
     - Unimplemented object service
   * - 2308
     - Data management policy violation
   * - 2400
     - Command failed
   * - 2500
     - Command failed; server closing connection
   * - 2501
     - Authentication error; server closing connection
   * - 2502
     - Session limit exceeded; server closing connection
