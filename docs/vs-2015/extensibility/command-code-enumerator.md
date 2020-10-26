---
title: コマンドコード列挙子 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- command code enumerator
- source control plug-ins, command code enumeration
ms.assetid: 5d2c360c-59e4-4da8-bcb4-dd07c7441e40
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 06f1a3f7146125e59d02efc72a4d4fc9ab33be39
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68184387"
---
# <a name="command-code-enumerator"></a>コマンド コードの列挙子
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

この列挙子は、 [SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md) のオプションで使用されます。また、 [SccPopulateList](../extensibility/sccpopulatelist-function.md)は、オプションが指定されているコマンドを示します。  
  
## <a name="syntax"></a>構文  
  
```  
enum SCCCOMMAND {  
   SCC_COMMAND_GET,  
   SCC_COMMAND_CHECKOUT,  
   SCC_COMMAND_CHECKIN,  
   SCC_COMMAND_UNCHECKOUT,  
   SCC_COMMAND_ADD,  
   SCC_COMMAND_REMOVE,  
   SCC_COMMAND_DIFF,  
   SCC_COMMAND_HISTORY,  
   SCC_COMMAND_RENAME,  
   SCC_COMMAND_PROPERTIES,  
   SCC_COMMAND_OPTIONS  
};  
```  
  
## <a name="members"></a>メンバー  
 SCC_COMMAND_GET  
 [Sccget](../extensibility/sccget-function.md)に対応します。  
  
 SCC_COMMAND_CHECKOUT  
 [Scccheckout](../extensibility/scccheckout-function.md)に対応します。  
  
 SCC_COMMAND_CHECKIN  
 [Scccheckin](../extensibility/scccheckin-function.md)に対応します。  
  
 SCC_COMMAND_UNCHECKOUT  
 [SccUncheckout](../extensibility/sccuncheckout-function.md)に対応します。  
  
 SCC_COMMAND_ADD  
 [Sccadd](../extensibility/sccadd-function.md)に対応します。  
  
 SCC_COMMAND_REMOVE  
 [Sccremove](../extensibility/sccremove-function.md)に対応します。  
  
 SCC_COMMAND_DIFF  
 [Sccdiff](../extensibility/sccdiff-function.md)に対応します。  
  
 SCC_COMMAND_HISTORY  
 [SccHistory](../extensibility/scchistory-function.md)に対応します。  
  
 SCC_COMMAND_RENAME  
 [Sccrename](../extensibility/sccrename-function.md)に対応します。  
  
 SCC_COMMAND_PROPERTIES  
 [Sccproperties](../extensibility/sccproperties-function.md)に対応します。  
  
 SCC_COMMAND_OPTIONS  
 [Sccsetoption](../extensibility/sccsetoption-function.md)に対応します。  
  
## <a name="see-also"></a>参照  
 [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)   
 [SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md)   
 [SccPopulateList](../extensibility/sccpopulatelist-function.md)
