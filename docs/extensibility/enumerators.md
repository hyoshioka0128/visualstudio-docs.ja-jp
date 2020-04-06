---
title: 列挙子 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, enumerators
ms.assetid: a60030c5-e1d1-47e1-84bb-cbfe838ab479
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ee48d064612e5519d5ad7e5eaf04de6c5a697837
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711855"
---
# <a name="enumerators"></a>列挙子
このセクションでは、ソース管理プラグインが知る必要があるソース管理プラグイン API の列挙子データ型を示します。

## <a name="in-this-section"></a>このセクションの内容
- [コマンド コード](../extensibility/command-code-enumerator.md)関数の[オプション](../extensibility/sccgetcommandoptions-function.md)[を列挙します](../extensibility/sccpopulatelist-function.md)。

- [メッセージ](../extensibility/message-enumerator.md)印刷コールバックに使用されるフラグを列挙[します](../extensibility/lptextoutproc.md)。

- [ファイルステータスコード](../extensibility/file-status-code-enumerator.md)ソース管理下のファイルの状態を指定する名前付き定数値を格納します。

- [ディレクトリステータスコード](../extensibility/directory-status-code-enumerator.md)ソース管理下のディレクトリの状態を指定する名前付き定数値を格納します。

## <a name="related-sections"></a>関連項目
- [ソース管理プラグインを作成する](../extensibility/internals/creating-a-source-control-plug-in.md)ソース管理プラグイン SDK を定義し、含まれているリソースについて説明します。

- [コマンドオプション](../extensibility/sccgetcommandoptions-function.md)指定したコマンドの詳細オプションをユーザーに求めます。

- [一覧](../extensibility/sccpopulatelist-function.md)ファイルのリストで現在のステータスを調べます。 また、ファイルが`pfnPopulate`の条件に一致しない場合に、この関数を使用して呼`nCommand`び出し元に通知します。

- [を実行します。](../extensibility/lptextoutproc.md)ソース管理プラグインからのメッセージを IDE で表示するために[SccOpenProject](../extensibility/sccopenproject-function.md)によって使用されるコールバック関数について説明します。

- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)ソース管理プラグイン API のすべての要素の完全な一覧を提供します。
