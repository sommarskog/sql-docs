---
title: Using Data Classification ODBC driver
description: Learn how to use Data Classification with the ODBC driver and how to incorporate your data protection policies into your ODBC application.
author: "v-makouz"
ms.author: v-makouz
ms.reviewer: v-davidengel
ms.date: "06/15/2023"
ms.service: sql
ms.subservice: connectivity
ms.topic: conceptual
helpviewer_keywords:
  - "driver"
---
# Data Classification

[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## Overview

For managing sensitive data, SQL Server and Azure SQL Server introduced the ability to provide database columns with sensitivity metadata that allows the client application to handle different types of sensitive data (such as health, financial, etc.) in accordance with data protection policies.

For more information on how to assign classification to columns, see [SQL Data Discovery and Classification](../../relational-databases/security/sql-data-discovery-and-classification.md).

Microsoft ODBC Driver 17.2 or later allows the retrieval of this metadata via SQLGetDescField using the SQL_CA_SS_DATA_CLASSIFICATION field identifier.

## Format

SQLGetDescField has the following syntax:

```cpp
SQLRETURN SQLGetDescField(  
     SQLHDESC        DescriptorHandle,  
     SQLSMALLINT     RecNumber,  
     SQLSMALLINT     FieldIdentifier,  
     SQLPOINTER      ValuePtr,  
     SQLINTEGER      BufferLength,  
     SQLINTEGER *    StringLengthPtr);  
```

*DescriptorHandle*  
 [Input] IRD (Implementation Row Descriptor) handle. Can be retrieved by a call to SQLGetStmtAttr with SQL_ATTR_IMP_ROW_DESC statement attribute
  
 *RecNumber*  
 [Input] 0
  
 *FieldIdentifier*  
 [Input] SQL_CA_SS_DATA_CLASSIFICATION
  
 *ValuePtr*  
 [Output] Output buffer
  
 *BufferLength*  
 [Input] Length of output buffer in bytes

 *StringLengthPtr*
 [Output] Pointer to the buffer in which to return the total number of bytes available to return in *ValuePtr*.

> [!NOTE]
> If the size of the buffer is unknown, it can be determined by calling SQLGetDescField with *ValuePtr* as NULL and examining the value of *StringLengthPtr*.

If Data Classification information isn't available, an *Invalid Descriptor Field* error will be returned.

Upon a successful call to SQLGetDescField, the buffer pointed to by *ValuePtr* will contain the following data:

 `nn nn [n sensitivitylabels] tt tt [t informationtypes] cc cc [c columnsensitivitys]`

> [!NOTE]
> `nn nn`, `tt tt`, and `cc cc` are multibyte integers, which are stored with the least significant byte at the lowest address.

*`sensitivitylabel`* and *`informationtype`*  are both of the form

 `nn [n bytes name] ii [i bytes id]`

*`columnsensitivity`* is of the form

 `nn nn [n sensitivityprops]`

For each column *(c)*, *n* 4-byte *`sensitivityprops`* are present:

 `ss ss tt tt`

s - index into the *`sensitivitylabels`* array, `FF FF` if not labeled

t - index into the *`informationtypes`* array, `FF FF` if not labeled

<br><br>
The format of the data can be expressed as the following pseudo-structures:

```cpp
struct IDnamePair {
 BYTE nameLen;
 USHORT name[nameLen];
 BYTE idLen;
 USHORT id[idLen];
};

struct SensitivityProp {
 USHORT labelIdx;
 USHORT infoTypeIdx;
};

USHORT nLabels;
struct IDnamePair labels[nLabels];
USHORT nInfoTypes;
struct IDnamePair infotypes[nInfoTypes];
USHORT nColumns;
struct {
 USHORT nProps;
 struct SensitivityProp[nProps];
} columnClassification[nColumns];
```

## Code sample

Test application that demonstrates how to read Data Classification metadata. On Windows it can be compiled using `cl /MD dataclassification.c /I (directory of msodbcsql.h) /link odbc32.lib` and run with a connection string, and a SQL query (that returns classified columns) as parameters:

```cpp
#ifdef _WIN32
#include <windows.h>
#endif
#include <sql.h>
#include <sqlext.h>
#include <msodbcsql.h>
#include <stdio.h>
SQLHANDLE env, dbc, stmt;
void checkRC_exit(SQLRETURN rc, SQLHANDLE hand, SQLSMALLINT htype, int retcode, char *action)
{
    if ((rc == SQL_ERROR || rc == SQL_SUCCESS_WITH_INFO) && hand)
    {
        char msg[1024], state[6];
        int i = 0;
        SQLRETURN rc2;
        SQLINTEGER err;
        SQLSMALLINT lenout;
        while ((rc2 = SQLGetDiagRec(htype, hand, ++i, state, &err, msg, sizeof(msg), &lenout)) == SQL_SUCCESS ||
            rc2 == SQL_SUCCESS_WITH_INFO)
            printf("%d (%d)[%s]%s\n", i, err, state, msg);
    }
    if (rc == SQL_ERROR && retcode)
    {
        printf("Error occurred%s%s\n", action ? " upon " : "", action ? action : "");
        exit(retcode);
    }
}
void printLabelInfo(char *type, char **pptr)
{
    char *ptr = *pptr;
    unsigned short nlabels;
    printf("----- %s(%u) -----\n", type, nlabels = *(unsigned short*)ptr);
    ptr += sizeof(unsigned short);
    while (nlabels--)
    {
        int namelen, idlen;
        char *nameptr, *idptr;
        namelen = *ptr++;
        nameptr = ptr;
        ptr += namelen * 2;
        idlen = *ptr++;
        idptr = ptr;
        ptr += idlen * 2;
        wprintf(L"Name: \"%.*s\" Id: \"%.*s\"\n", namelen, nameptr, idlen, idptr);
    }
    *pptr = ptr;
}
int main(int argc, char **argv)
{
    unsigned char *dcbuf;
    unsigned int dclen = 0;
    SQLRETURN rc;
    SQLHANDLE ird;
    if (argc < 3)
    {
        fprintf(stderr, "usage: dataclassification connstr query\n");
        return 1;
    }
    checkRC_exit(SQLAllocHandle(SQL_HANDLE_ENV, 0, &env), 0, 0,
        2, "allocate environment");
    checkRC_exit(SQLSetEnvAttr(env, SQL_ATTR_ODBC_VERSION, (SQLPOINTER)SQL_OV_ODBC3, 0), env, SQL_HANDLE_ENV,
        3, "set ODBC version");
    checkRC_exit(SQLAllocHandle(SQL_HANDLE_DBC, env, &dbc), env, SQL_HANDLE_ENV,
        4, "allocate connection");
    checkRC_exit(SQLDriverConnect(dbc, 0, argv[1], SQL_NTS, 0, 0, 0, SQL_DRIVER_NOPROMPT), dbc, SQL_HANDLE_DBC,
        5, "connect to server");
    checkRC_exit(SQLAllocHandle(SQL_HANDLE_STMT, dbc, &stmt), dbc, SQL_HANDLE_DBC,
        6, "allocate statement");
    checkRC_exit(SQLExecDirect(stmt, argv[2], SQL_NTS), stmt, SQL_HANDLE_STMT,
        7, "execute query");
    checkRC_exit(SQLGetStmtAttr(stmt, SQL_ATTR_IMP_ROW_DESC, (SQLPOINTER)&ird, SQL_IS_POINTER, 0), stmt, SQL_HANDLE_STMT,
        8, "get IRD handle");
    rc = SQLGetDescFieldW(ird, 0, SQL_CA_SS_DATA_CLASSIFICATION, dcbuf, 0, &dclen);

    checkRC_exit(rc, ird, SQL_HANDLE_DESC, 0, 0);
  

    SQLINTEGER dclenout;
    unsigned char *dcptr;
    unsigned short ncols;
    printf("Data Classification information (%u bytes):\n", dclen);
    if (!(dcbuf = malloc(dclen)))
    {
        printf("Memory Allocation Error");
        return 9;
    }
    checkRC_exit(SQLGetDescFieldW(ird, 0, SQL_CA_SS_DATA_CLASSIFICATION, dcbuf, dclen, &dclenout),
            ird, SQL_HANDLE_DESC, 10, "reading SQL_CA_SS_DATA_CLASSIFICATION");
    dcptr = dcbuf;
    printLabelInfo("Labels", &dcptr);
    printLabelInfo("Information Types", &dcptr);
    printf("----- Column Sensitivities(%u) -----\n", ncols = *(unsigned short*)dcptr);
    dcptr += sizeof(unsigned short);
    while (ncols--)
    {
        unsigned short nprops = *(unsigned short*)dcptr;
        dcptr += sizeof(unsigned short);
        while (nprops--)
        {
            unsigned short labelidx, typeidx;
            labelidx = *(unsigned short*)dcptr; dcptr += sizeof(unsigned short);
            typeidx = *(unsigned short*)dcptr; dcptr += sizeof(unsigned short);
            printf(labelidx == 0xFFFF ? "(none) " : "%u ", labelidx);
            printf(typeidx == 0xFFFF ? "(none)\n" : "%u\n", typeidx);
        }
        printf("-----\n");
    }
    if (dcptr != dcbuf + dclen)
    {
        printf("Error: unexpected parse of DATACLASSIFICATION data\n");
        return 11;
    }
    free(dcbuf);
    
    return 0;
}
```

## <a name="bkmk-version"></a>Supported Version

Microsoft ODBC Driver 17.2 allows the retrieval of Data Classification information via `SQLGetDescField` if `FieldIdentifier` is set to `SQL_CA_SS_DATA_CLASSIFICATION` (1237).

Starting from Microsoft ODBC Driver 17.4.1.1, it's possible to retrieve the version of Data Classification supported by a server via `SQLGetDescField` using the `SQL_CA_SS_DATA_CLASSIFICATION_VERSION` (1238) field identifier. In 17.4.1.1, the supported data classification version is set to "2".

Starting from 17.4.2.1, the default version of data classification is set to "1" and is the version the driver reports to SQL Server as supported. A new connection attribute `SQL_COPT_SS_DATACLASSIFICATION_VERSION` (1400) can allow application to change the supported version of Data Classification from "1" up to the maximum supported.

Example:

To set the version, this call should be made right before the SQLConnect or SQLDriverConnect call:

```cpp
ret = SQLSetConnectAttr(dbc, SQL_COPT_SS_DATACLASSIFICATION_VERSION, (SQLPOINTER)2, SQL_IS_INTEGER);
```

The value of the currently supported version of Data Classification can be retrieved via SQLGetConnectAttr call:

```cpp
ret = SQLGetConnectAttr(dbc, SQL_COPT_SS_DATACLASSIFICATION_VERSION, (SQLPOINTER)&dataClassVersion, SQL_IS_INTEGER, 0);
```
