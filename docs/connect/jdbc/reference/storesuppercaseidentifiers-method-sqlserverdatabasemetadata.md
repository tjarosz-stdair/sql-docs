---
title: "storesUpperCaseIdentifiers Method"
description: "storesUpperCaseIdentifiers Method (SQLServerDatabaseMetaData)"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.prod: sql
ms.technology: connectivity
ms.topic: reference
apilocation: "sqljdbc.jar"
apiname: "SQLServerDatabaseMetaData.storesUpperCaseIdentifiers"
apitype: "Assembly"
---
# storesUpperCaseIdentifiers Method (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retrieves whether this database treats mixed-case SQL identifiers that are not enclosed in quotation marks as case-insensitive and stores them in uppercase.  
  
## Syntax  
  
```  
  
public boolean storesUpperCaseIdentifiers()  
```  
  
## Return Value  
 **true** if the identifiers are stored in uppercase. Otherwise, **false**.  
  
## Exceptions  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## Remarks  
 This storesUpperCaseIdentifiers method is specified by the storesUpperCaseIdentifiers method in the java.sql.DatabaseMetaData interface.  
  
## See Also  
 [SQLServerDatabaseMetaData Methods](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData Members](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData Class](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
