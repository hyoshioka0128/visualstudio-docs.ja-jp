---
title: コマンド コード列挙子 |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739785"
---
# <a name="command-code-enumerator"></a>コマンド コード列挙子
この列挙子は、オプションを指定するコマンドを示すために[、SccGet コマンド オプション](../extensibility/sccgetcommandoptions-function.md)と[SccPopulateList](../extensibility/sccpopulatelist-function.md)のオプションで使用されます。

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
SCC_COMMAND_GET [SccGet](../extensibility/sccget-function.md)に対応しています。

SCC_COMMAND_CHECKOUT [SccCheckout](../extensibility/scccheckout-function.md)に対応しています。

SCC_COMMAND_CHECKIN [SccCheckin](../extensibility/scccheckin-function.md)に対応しています。

SCC_COMMAND_UNCHECKOUT [SccUncheckout](../extensibility/sccuncheckout-function.md)に対応しています。

SCC_COMMAND_ADD [SccAdd](../extensibility/sccadd-function.md)に対応しています。

SCC_COMMAND_REMOVE [SccRemove](../extensibility/sccremove-function.md)に対応しています。

SCC_COMMAND_DIFF [SccDiff](../extensibility/sccdiff-function.md)に対応しています。

SCC_COMMAND_HISTORY [SccHistory](../extensibility/scchistory-function.md)に対応しています。

SCC_COMMAND_RENAME 名前の[変更](../extensibility/sccrename-function.md)に対応します。

SCC_COMMAND_PROPERTIES [SccProperties](../extensibility/sccproperties-function.md)に対応しています。

[SCC_COMMAND_OPTIONSSccSet オプション](../extensibility/sccsetoption-function.md)に対応しています。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
- [SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md)
- [SccPopulateList](../extensibility/sccpopulatelist-function.md)
