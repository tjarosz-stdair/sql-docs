---
title: "ntext, text, and image (Transact-SQL)"
description: "The ntext, text, and image data types are deprecated data types for storing large non-Unicode and Unicode character and binary data."
author: MikeRayMSFT
ms.author: mikeray
ms.date: "04/13/2022"
ms.prod: sql
ms.technology: t-sql
ms.topic: "reference"
f1_keywords:
  - "ntext_TSQL"
  - "ntext"
helpviewer_keywords:
  - "text data type, about text data type"
  - "text [SQL Server], data types"
  - "ntext data type"
  - "ntext data type, about ntext data type"
  - "image data type, about image data type"
dev_langs:
  - "TSQL"
---
# ntext, text, and image (Transact-SQL)
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

Fixed and variable-length data types for storing large non-Unicode and Unicode character and binary data. Unicode data uses the UNICODE UCS-2 character set.
  
> [!IMPORTANT]
> The **ntext**, **text**, and **image** data types will be removed in a future version of SQL Server. Avoid using these data types in new development work, and plan to modify applications that currently use them. Use [nvarchar(max)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md), [varchar(max)](../../t-sql/data-types/char-and-varchar-transact-sql.md), and [varbinary(max)](../../t-sql/data-types/binary-and-varbinary-transact-sql.md) instead.  
  
## Arguments
**ntext**  
Variable-length Unicode data with a maximum string length of 2^30 - 1 (1,073,741,823) bytes. Storage size, in bytes, is two times the string length that is entered. The ISO synonym for **ntext** is **national text**.
  
**text**  
Variable-length non-Unicode data in the code page of the server and with a maximum string length of 2^31-1 (2,147,483,647). When the server code page uses double-byte characters, the storage is still 2,147,483,647 bytes. Depending on the character string, the storage size may be less than 2,147,483,647 bytes.
  
**image**  
Variable-length binary data from 0 through 2^31-1 (2,147,483,647) bytes.
  
## Remarks  
The following functions and statements can be used with **ntext**, **text**, or **image** data.
  
|Functions|Statements|  
|---|---|
|[DATALENGTH &#40;Transact-SQL&#41;](../../t-sql/functions/datalength-transact-sql.md)|[READTEXT &#40;Transact-SQL&#41;](../../t-sql/queries/readtext-transact-sql.md)|  
|[PATINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)|[SET TEXTSIZE &#40;Transact-SQL&#41;](../../t-sql/statements/set-textsize-transact-sql.md)|  
|[SUBSTRING &#40;Transact-SQL&#41;](../../t-sql/functions/substring-transact-sql.md)|[UPDATETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/updatetext-transact-sql.md)|  
|[TEXTPTR &#40;Transact-SQL&#41;](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md)|[WRITETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/writetext-transact-sql.md)|  
|[TEXTVALID &#40;Transact-SQL&#41;](../../t-sql/functions/text-and-image-functions-textvalid-transact-sql.md)||  

> [!CAUTION]
> When dropping columns using the deprecated NTEXT data type, the cleanup of the deleted data occurs as a serialized operation on all rows. The cleanup can require a large amount of time. When dropping an NTEXT column in a table with lots of rows, update the NTEXT column to NULL value first, then drop the column. You can run this option with parallel operations and make it much faster.

## See also
- [Data Types &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
- [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)  
- [SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
- [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)

## Next steps

- [CAST and CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
- [Data Type Conversion &#40;Database Engine&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
- [ALTER TABLE (Transact-SQL)](../statements/alter-table-transact-sql.md)