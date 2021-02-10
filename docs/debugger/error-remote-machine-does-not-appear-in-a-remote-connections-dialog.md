---
title: リモート コンピューターが [リモート接続] ダイアログに表示されない | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: be39d733b2e5fe83fa9f7e2241c7de06980bb583
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99871368"
---
# <a name="error-remote-machine-does-not-appear-in-a-remote-connections-dialog"></a>エラー :リモート コンピューターが [リモート接続] ダイアログに表示されません
リモート コンピューターが [リモート接続] ダイアログ ボックスに表示されない場合、下記の一般的な原因を確認してください。

 マネージド互換モードを使用している場合は、Visual Studio 2010 用のマニュアル:「[リモート デバッグのトラブルシューティング - Visual Studio 2010](/previous-versions/visualstudio/visual-studio-2010/2ys11ead(v=vs.100))」を調べてください。

### <a name="common-causes-for-this-error"></a>このエラーの一般的な原因

- リモート コンピューターが別のサブネット内に存在するコンピューター上で実行されています。 この問題を解決するには、[修飾子] ダイアログ ボックスで、コンピューター名または IP アドレスを手動で入力します。

- リモート デバッガーがリモート コンピューター上で実行されていません。 この問題を解決するには、リモート デバッガーを起動します。

- ファイアウォールで、Visual Studio とリモート コンピューター間の通信がブロックされています。 これを解決するには、Visual Studio とリモート デバッガー (msvsmon) の通信を許可するようにファイアウォールを構成します。

- ウイルス対策ソフトウェアで、Visual Studio とリモート コンピューター間の通信がブロックされています。 これを解決するには、Visual Studio とリモート デバッガー (msvsmon) の通信を許可するようにウイルス対策ソフトウェアを構成します。

## <a name="see-also"></a>関連項目
- [Remote Debugging](../debugger/remote-debugging.md)