---
title: QUERYて FUNC |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- QUERYCHANGESFUNC
helpviewer_keywords:
- QUERYCHANGESFUNC callback function
- QUERYCHANGESDATA structure
ms.assetid: 9d383e2c-eee1-4996-973a-0652d4c5951c
caps.latest.revision: 17
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 42f901fa31b3b682c7e19c98f5707adb3b4fb3f3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68193852"
---
# <a name="querychangesfunc"></a>QUERYCHANGESFUNC
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

これは、ファイル名のコレクションを列挙し、各ファイルの状態を特定するために [Sccquerychanges](../extensibility/sccquerychanges-function.md) 操作によって使用されるコールバック関数です。  
  
 `SccQueryChanges`関数には、ファイルの一覧とコールバックへのポインターが指定されてい `QUERYCHANGESFUNC` ます。 ソース管理プラグインは、指定されたリストを列挙し、リスト内の各ファイルについて (このコールバックによって) 状態を提供します。  
  
## <a name="signature"></a>署名  
  
```cpp#  
typedef BOOL (*QUERYCHANGESFUNC)(  
   LPVOID pvCallerData,  
   QUERYCHANGESDATA * pChangesData  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 pvCallerData  
 から `pvCallerData` 呼び出し元 (IDE) によって [Sccquerychanges](../extensibility/sccquerychanges-function.md)によって渡されるパラメーター。 ソース管理プラグインは、この値の内容についての想定を行いません。  
  
 Pにデータを  
 からファイルへの変更を記述する [querychanges データ構造](#LinkQUERYCHANGESDATA) 体へのポインター。  
  
## <a name="return-value"></a>戻り値  
 IDE から適切なエラーコードが返されます。  
  
|値|説明|  
|-----------|-----------------|  
|SCC_OK|処理し続けます。|  
|SCC_I_OPERATIONCANCELED|処理を停止します。|  
|SCC_E_xxx|適切な SCC エラーが発生すると処理が停止します。|  
  
## <a name="querychangesdata-structure"></a><a name="LinkQUERYCHANGESDATA"></a> QUERYのデータ構造  
 各ファイルに渡される構造は、次のようになります。  
  
```cpp#  
struct QUERYCHANGESDATA_A  
{  
    DWORD  dwSize;  
    LPCSTR lpFileName;  
    DWORD  dwChangeType;  
    LPCSTR lpLatestName;  
};  
  
typedef struct QUERYCHANGESDATA_A QUERYCHANGESDATA;  
  
struct QUERYCHANGESDATA_W  
{  
    DWORD   dwSize;  
    LPCWSTR lpFileName;  
    DWORD   dwChangeType;  
    LPCWSTR lpLatestName;  
};  
```  
  
 dwSize  
 この構造体のサイズ (バイト単位)。  
  
 lpFileName  
 この項目の元のファイル名。  
  
 dwChangeType  
 ファイルの状態を示すコード:  
  
|コード|説明|  
|----------|-----------------|  
|`SCC_CHANGE_UNKNOWN`|変更内容を識別できません。|  
|`SCC_CHANGE_UNCHANGED`|このファイルの名前を変更することはできません。|  
|`SCC_CHANGE_DIFFERENT`|ファイルの id が異なりますが、同じ名前がデータベース内に存在します。|  
|`SCC_CHANGE_NONEXISTENT`|ファイルがデータベースまたはローカルに存在しません。|  
|`SCC_CHANGE_DATABASE_DELETED`|ファイルがデータベースで削除されました。|  
|`SCC_CHANGE_LOCAL_DELETED`|ファイルはローカルで削除されましたが、ファイルはデータベースにまだ存在します。 これを特定できない場合は、を返し `SCC_CHANGE_DATABASE_ADDED` ます。|  
|`SCC_CHANGE_DATABASE_ADDED`|ファイルはデータベースに追加されましたが、ローカルには存在しません。|  
|`SCC_CHANGE_LOCAL_ADDED`|ファイルがデータベースに存在せず、新しいローカルファイルです。|  
|`SCC_CHANGE_RENAMED_TO`|ファイル名が変更されたか、データベースでとして移動されました `lpLatestName` 。|  
|`SCC_CHANGE_RENAMED_FROM`|データベース内のファイルの名前が変更または移動されまし `lpLatestName` た。この値を追跡するにはコストがかかりすぎる場合は、などの別のフラグを返し `SCC_CHANGE_DATABASE_ADDED` ます。|  
  
 lpLatestName  
 この項目の現在のファイル名。  
  
## <a name="see-also"></a>参照  
 [IDE によって実装されるコールバック関数](../extensibility/callback-functions-implemented-by-the-ide.md)   
 [SccQueryChanges](../extensibility/sccquerychanges-function.md)   
 [エラー コード](../extensibility/error-codes.md)
