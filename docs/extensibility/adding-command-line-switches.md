---
title: Command-Line スイッチの追加 |Microsoft Docs
description: devenv.exe コマンドの実行時に VSPackage に適用されるコマンドラインスイッチを追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- command-line switches, adding
- command-line switches, retrieving
- IVsAppCommandLine::GetOption method
- command line, switches
ms.assetid: 8bbbd87e-76fe-4fb5-8ef9-65f5e31967cf
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: fa38e508c087d61ad5ea1762e3e3cc33d6d4f538
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99939228"
---
# <a name="add-command-line-switches"></a>コマンドラインスイッチの追加
*devenv.exe* の実行時に、VSPackage に適用するコマンドラインスイッチを追加できます。 <xref:Microsoft.VisualStudio.Shell.ProvideAppCommandLineAttribute>スイッチとそのプロパティの名前を宣言するには、を使用します。 この例では、 **Addcommandswitchpackage** という名前の VSPackage のサブクラスの MySwitch スイッチが追加され、引数と VSPackage が自動的に読み込まれます。

```csharp
[ProvideAppCommandLine("MySwitch", typeof(AddCommandSwitchPackage), Arguments = "0", DemandLoad = 1)]
```

 名前付きパラメーターについては、次の説明を参照してください。

|名前|説明|
|-|-|
| 引数 | スイッチの引数の数。 "*"、または引数のリストを指定できます。 |
| DemandLoad | このが1に設定されている場合は、VSPackage を自動的に読み込みます。それ以外の場合は0に設定します。 |
| HelpString | **Devenv/?** で表示する文字列のヘルプ文字列またはリソース ID。 |
| 名前 | スイッチ。 |
| PackageGuid | パッケージの GUID。 |

 引数の最初の値は、通常は0または1です。 特別な値 ' * ' を使用すると、コマンドラインの残りの部分が引数であることを示すことができます。 これは、ユーザーがデバッガーのコマンド文字列を渡す必要があるデバッグシナリオに役立ちます。

 DemandLoad の値は `true` (1) または `false` (0) VSPackage を自動的に読み込む必要があることを示します。

 HelpString 値は、 **devenv/?** に表示される文字列のリソース ID です。 ヘルプの表示。 この値は、"#nnn" の形式にする必要があります。 nnn は整数です。 リソースファイル内の文字列値は、改行文字で終わる必要があります。

 名前の値はスイッチの名前です。

 PackageGuid 値は、このスイッチを実装するパッケージの GUID です。 IDE では、この GUID を使用して、コマンドラインスイッチが適用されるレジストリ内の VSPackage を検索します。

## <a name="retrieve-command-line-switches"></a>コマンドラインスイッチを取得する
 パッケージが読み込まれたら、次の手順を完了してコマンドラインスイッチを取得できます。

1. VSPackage の実装で <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A> 、でを呼び出して、 `QueryService` インターフェイスを取得し <xref:Microsoft.VisualStudio.Shell.Interop.SVsAppCommandLine> <xref:Microsoft.VisualStudio.Shell.Interop.IVsAppCommandLine> ます。

2. を呼び出して、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAppCommandLine.GetOption%2A> ユーザーが入力したコマンドラインスイッチを取得します。

   次のコードは、MySwitch コマンドラインスイッチがユーザーによって入力されたかどうかを調べる方法を示しています。

```csharp
IVsAppCommandLine cmdline = (IVsAppCommandLine)GetService(typeof(SVsAppCommandLine));

int isPresent = 0;
string optionValue = "";

cmdline.GetOption("MySwitch", out isPresent, out optionValue);
```

 パッケージが読み込まれるたびに、コマンドラインスイッチを確認する必要があります。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsAppCommandLine>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>
- [Devenv コマンドライン スイッチ](../ide/reference/devenv-command-line-switches.md)
- [CreatePkgDef ユーティリティ](../extensibility/internals/createpkgdef-utility.md)
- [.Pkgdef ファイル](https://devblogs.microsoft.com/visualstudio/whats-a-pkgdef-and-why/)
