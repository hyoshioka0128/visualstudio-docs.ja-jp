---
title: コマンド ライン スイッチを追加する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- command-line switches, adding
- command-line switches, retrieving
- IVsAppCommandLine::GetOption method
- command line, switches
ms.assetid: 8bbbd87e-76fe-4fb5-8ef9-65f5e31967cf
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3f2df3a704c34d97c9d5acfa72249fe492b7f812
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740165"
---
# <a name="add-command-line-switches"></a>コマンド ライン スイッチを追加する
*devenv.exe*が実行されたときに VSPackage に適用されるコマンド ライン スイッチを追加できます。 スイッチ<xref:Microsoft.VisualStudio.Shell.ProvideAppCommandLineAttribute>の名前とプロパティを宣言するために使用します。 この例では、引数を持たないと自動的に読み込まれた VSPackage との間で **、AddCommandSwitchPackage**という名前の VSPackage のサブクラスに対して、MySwitch スイッチが追加されます。

```csharp
[ProvideAppCommandLine("MySwitch", typeof(AddCommandSwitchPackage), Arguments = "0", DemandLoad = 1)]
```

 名前付きパラメーターを以下の説明に示します。

||||
|-|-|-|-|
| パラメーター | 説明|
| 引数 | スイッチの引数の数。 "*" または引数のリストを指定できます。 |
| デマンドロード | 1 に設定されている場合は自動的に VSPackage を読み込み、それ以外の場合は 0 に設定します。 |
| Helpstring | **devenv /?** で表示する文字列のヘルプ文字列またはリソース ID。 |
| 名前 | スイッチ。 |
| パッケージGuid | パッケージの GUID。 |

 引数の最初の値は、通常 0 または 1 です。 コマンド行の残りの部分全体が引数であることを示すために、特殊値 '*' を使用できます。 これは、ユーザーがデバッガーコマンド文字列を渡す必要があるシナリオをデバッグする場合に役立ちます。

 デマンド ロード値`true`は (1) または`false`(0) は、VSPackage が自動的に読み込まれる必要があることを示します。

 ヘルプ文字列値は **、devenv /?** ヘルプ表示。 この値は、nnn が整数である場合に"#nnn"の形式にする必要があります。 リソース ファイル内の文字列値は、改行文字で終わる必要があります。

 Name 値はスイッチの名前です。

 値は、このスイッチを実装するパッケージの GUID です。 IDE では、コマンド ライン スイッチが適用されるレジストリで VSPackage を検索するのにこの GUID を使用します。

## <a name="retrieve-command-line-switches"></a>コマンド ライン スイッチの取得
 パッケージが読み込まれると、次の手順を実行してコマンド ライン スイッチを取得できます。

1. VSPackage<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>の実装で、`QueryService`インターフェイス<xref:Microsoft.VisualStudio.Shell.Interop.SVsAppCommandLine>を取得する呼び<xref:Microsoft.VisualStudio.Shell.Interop.IVsAppCommandLine>出しします。

2. ユーザー<xref:Microsoft.VisualStudio.Shell.Interop.IVsAppCommandLine.GetOption%2A>が入力したコマンド ライン スイッチを取得する呼び出し。

   次のコードは、ユーザーが MySwitch コマンド ライン スイッチを入力したかどうかを確認する方法を示しています。

```csharp
IVsAppCommandLine cmdline = (IVsAppCommandLine)GetService(typeof(SVsAppCommandLine));

int isPresent = 0;
string optionValue = "";

cmdline.GetOption("MySwitch", out isPresent, out optionValue);
```

 パッケージが読み込まれるたびに、コマンド ライン スイッチを確認するのは、ユーザーの責任です。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsAppCommandLine>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>
- [Devenv コマンドライン スイッチ](../ide/reference/devenv-command-line-switches.md)
- [ユーティリティを作成します。](../extensibility/internals/createpkgdef-utility.md)
- [.Pkgdef ファイル](https://devblogs.microsoft.com/visualstudio/whats-a-pkgdef-and-why/)
