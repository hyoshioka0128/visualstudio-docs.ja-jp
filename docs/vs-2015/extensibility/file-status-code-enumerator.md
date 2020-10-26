---
title: ファイル状態コード列挙子 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- named constants, SccStatus enumerator
- source control plug-ins, file status enumeration
- SccStatus enumerator
- file status code enumerator
ms.assetid: 5c37876b-c83c-4ca1-837b-57cd465a879a
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1b6e74caa9eedd42e25339d62f5837ccfe82d001
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204381"
---
# <a name="file-status-code-enumerator"></a>ファイルのステータス コードの列挙子
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

列挙子には、 `SccStatus` ソース管理システム内のファイルの状態を指定する名前付き定数値が含まれます。 この列挙体は、 [Sccqueryinfo](../extensibility/sccqueryinfo-function.md) およびコールバック関数によって使用され `POPLISTFUNC` ます (詳細については、 [POPLISTFUNC](../extensibility/poplistfunc.md) を参照してください)。  
  
## <a name="syntax"></a>構文  
  
```  
enum SccStatus {  
   SCC_STATUS_INVALID          = -1L,  
   SCC_STATUS_NOTCONTROLLED    = 0x0000L,  
   SCC_STATUS_CONTROLLED       = 0x0001L,  
   SCC_STATUS_CHECKEDOUT       = 0x0002L,  
   SCC_STATUS_OUTOTHER         = 0x0004L,  
   SCC_STATUS_OUTEXCLUSIVE     = 0x0008L,  
   SCC_STATUS_OUTMULTIPLE      = 0x0010L,  
   SCC_STATUS_OUTOFDATE        = 0x0020L,  
   SCC_STATUS_DELETED          = 0x0040L,  
   SCC_STATUS_LOCKED           = 0x0080L,  
   SCC_STATUS_MERGED           = 0x0100L,  
   SCC_STATUS_SHARED           = 0x0200L,  
   SCC_STATUS_PINNED           = 0x0400L,  
   SCC_STATUS_MODIFIED         = 0x0800L,  
   SCC_STATUS_OUTBYUSER        = 0x1000L  
   SCC_STATUS_NOMERGE          = 0x2000L  
   SCC_STATUS_RESERVED_1       = 0x4000L  
   SCC_STATUS_RESERVED_2       = 0x8000L  
};  
```  
  
## <a name="members"></a>メンバー  
 SCC_STATUS_INVALID  
 状態を取得できませんでした。それに依存しないでください。  
  
 SCC_STATUS_NOTCONTROLLED  
 ファイルがソース管理下にありません。  
  
 SCC_STATUS_CONTROLLED  
 ファイルはソース管理下にあります。  
  
 SCC_STATUS_CHECKEDOUT  
 ローカルディスクの現在のユーザーによってチェックアウトされました。  
  
 SCC_STATUS_OUTOTHER  
 ファイルは別のユーザーによってチェックアウトされています。  
  
 SCC_STATUS_OUTEXCLUSIVE  
 ファイルは排他的にチェックアウトされています。  
  
 SCC_STATUS_OUTMULTIPLE  
 複数のユーザーによってファイルがチェックアウトされています。  
  
 SCC_STATUS_OUTOFDATE  
 ファイルが最新ではありません。  
  
 SCC_STATUS_DELETED  
 ファイルがプロジェクトから削除されました。  
  
 SCC_STATUS_LOCKED  
 ファイルがロックされています。これ以上のバージョンは使用できません。  
  
 SCC_STATUS_MERGED  
 ファイルはマージされましたが、まだ修正または検証されていません。  
  
 SCC_STATUS_SHARED  
 ファイルはプロジェクト間で共有されます。  
  
 SCC_STATUS_PINNED  
 ファイルは明示的なバージョンで共有されています。  
  
 SCC_STATUS_MODIFIED  
 ファイルが変更されたか、壊れているか、違反しています。  
  
 SCC_STATUS_OUTBYUSER  
 ファイルは現在のユーザーによってチェックアウトされています。  
  
 SCC_STATUS_NOMERGE  
 ファイルはとマージできません。また、GET の前に保存する必要もありません。  
  
 SCC_STATUS_RESERVED_1  
 内部使用のために予約されています。  
  
 SCC_STATUS_RESERVED_2  
 内部使用のために予約されています。  
  
## <a name="see-also"></a>参照  
 [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)   
 [SccQueryInfo](../extensibility/sccqueryinfo-function.md)   
 [POPLISTFUNC](../extensibility/poplistfunc.md)
