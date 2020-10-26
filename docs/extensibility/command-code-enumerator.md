---
title: コマンドコード列挙子 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- command code enumerator
- source control plug-ins, command code enumeration
ms.assetid: 5d2c360c-59e4-4da8-bcb4-dd07c7441e40
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 15916d26ac0120417205af0bb9117a45ec0397c6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80739785"
---
# <a name="command-code-enumerator"></a>コマンドコードの列挙子
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
SCC_COMMAND_GET は [Sccget](../extensibility/sccget-function.md)に対応します。

SCC_COMMAND_CHECKOUT は [Scccheckout](../extensibility/scccheckout-function.md)に相当します。

SCC_COMMAND_CHECKIN は [Scccheckin](../extensibility/scccheckin-function.md)に相当します。

SCC_COMMAND_UNCHECKOUT は [SccUncheckout](../extensibility/sccuncheckout-function.md)に対応します。

SCC_COMMAND_ADD は [Sccadd](../extensibility/sccadd-function.md)に対応します。

SCC_COMMAND_REMOVE は [Sccremove](../extensibility/sccremove-function.md)に対応します。

SCC_COMMAND_DIFF は [Sccdiff](../extensibility/sccdiff-function.md)に対応します。

SCC_COMMAND_HISTORY は [SccHistory](../extensibility/scchistory-function.md)に対応します。

SCC_COMMAND_RENAME は [Sccrename](../extensibility/sccrename-function.md)に対応します。

SCC_COMMAND_PROPERTIES は [Sccproperties](../extensibility/sccproperties-function.md)に対応します。

SCC_COMMAND_OPTIONS は [Sccsetoption](../extensibility/sccsetoption-function.md)に対応します。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
- [SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md)
- [SccPopulateList](../extensibility/sccpopulatelist-function.md)
