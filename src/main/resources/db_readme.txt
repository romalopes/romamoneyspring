================================================================================
===        Roma Money Spring application - Database Configuration      ===
================================================================================

@author Anderson Lopes (romalopes)

--------------------------------------------------------------------------------

In its default configuration, RomaMoneySpring uses an in-memory database (HSQLDB) which
gets populated at startup with data. A similar setup is provided for Mysql in case
a persistent database configuration is needed.
Note that whenever the database type is changed, the jdbc.properties file needs to
be updated.