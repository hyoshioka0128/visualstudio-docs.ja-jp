---
title: -Command (devenv.exe)
ms.date: 12/10/2018
ms.topic: reference
helpviewer_keywords:
- Devenv, /Command switch
- /Command Devenv switch
- Command Devenv switch
ms.assetid: 13c20cd6-f09d-400a-8b7b-ecc266a32cef
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 434b2ad0f2a6ca4d84c6d82bf9a1a85876a4d975
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75570402"
---
# <a name="command-devenvexe"></a>/Command (devenv.exe)

Visual Studio IDE を起動した後、指定したコマンドを実行します。

## <a name="syntax"></a>構文

```shell
devenv /Command CommandName
```

## <a name="arguments"></a>引数

*CommandName*

必須です。 Visual Studio コマンドの完全な名前またはその別名を二重引用符で囲みます。 コマンドとエイリアスの構文について詳しくは、「[Visual Studio のコマンド](../../ide/reference/visual-studio-commands.md)」をご覧ください。

## <a name="remarks"></a>Remarks

起動が完了すると、指定したコマンドが IDE で実行されます。

::: moniker range="vs-2017"

このスイッチを使用すると、起動時に IDE にスタート ページが表示されません。

::: moniker-end

アドインでコマンドが公開されている場合は、このスイッチを使ってコマンド ラインからアドインを起動できます。 詳細については、[アドイン マネージャーを使用してアドインを制御する](/previous-versions/xwdatdwh(v=vs.140))」をご覧ください。

## <a name="example"></a>例

最初の例では、Visual Studio を起動し、Open Favorite Files マクロを自動的に実行します。

2 番目の例では、Web を参照するタブを IDE 内で開き、Microsoft Docs のサイトに移動します。

3 番目の例では、`some_file.cs` という名前の新しいファイルを作成し、それをコード エディターで開きます。

```shell
devenv /command "Macros.MyMacros.Module1.OpenFavoriteFiles"

devenv /command "navigate https://docs.microsoft.com/"

devenv /command "nf some_file.cs"
```

## <a name="see-also"></a>関連項目

- [Devenv コマンドライン スイッチ](../../ide/reference/devenv-command-line-switches.md)
- [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)
- [コマンド ウィンドウ](command-window.md)
