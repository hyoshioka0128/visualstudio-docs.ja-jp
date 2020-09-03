---
title: ディレクトリ状態コード列挙子 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- directory status code enumerator
- source control plug-ins, directory status enumeration
ms.assetid: 616026b5-f529-40ef-90c1-1836e116d797
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e082a691a389d5cb9a8fa307a627b11911e0db78
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68185255"
---
# <a name="directory-status-code-enumerator"></a>ディレクトリの状態コードの列挙子
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

列挙子には、 `SccDirStatus` ソース管理システム内のディレクトリの状態を指定する名前付き定数値が含まれます。 この列挙体は、 [Sccdirqueryinfo](../extensibility/sccdirqueryinfo-function.md)によって使用されます。 これは、ソース管理プラグイン API のバージョン1.2 で導入されました。  
  
## <a name="syntax"></a>構文  
  
```  
enum SccDirStatus {  
   SCC_DIRSTATUS_INVALID       = -1L,  
   SCC_DIRSTATUS_NOTCONTROLLED = 0x0000L,  
   SCC_DIRSTATUS_CONTROLLED    = 0x0001L,  
   SCC_DIRSTATUS_EMPTYPROJ     = 0x0002L  
};  
```  
  
## <a name="members"></a>メンバー  
 SCC_DIRSTATUS_INVALID  
 状態を取得できませんでした。それに依存しないでください。  
  
 SCC_DIRSTATUS_NOTCONTROLLED  
 ディレクトリがソース管理下にありません。  
  
 SCC_DIRSTATUS_CONTROLLED  
 ディレクトリはソース管理下にあります。  
  
 SCC_DIRSTATUS_EMPTYPROJ  
 このディレクトリに対応するプロジェクトが空です。  
  
## <a name="see-also"></a>参照  
 [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)   
 [SccDirQueryInfo](../extensibility/sccdirqueryinfo-function.md)
