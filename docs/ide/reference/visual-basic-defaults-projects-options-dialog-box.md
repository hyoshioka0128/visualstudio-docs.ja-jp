---
title: '[Visual Basic の既定値] ([オプション] ダイアログ ボックス - [プロジェクト])'
description: '[プロジェクトおよびソリューション] セクションの [Visual Basic の既定値] ページを使用して、Visual Basic プロジェクトのオプションに対する既定の設定を指定する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Projects.VBDefaults
helpviewer_keywords:
- Option Explicit statement, setting in the IDE
- Option Compare statement, setting in the IDE
- Option Strict statement, setting in the IDE
ms.assetid: 2465cd9d-18b6-4c4a-b1ea-86dbab23fc79
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 3de415f99dbb9a91f2fa0e30ffc5e40727d10303
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99889748"
---
# <a name="visual-basic-defaults-projects-options-dialog-box"></a>[Visual Basic の既定値] ([オプション] ダイアログ ボックス - [プロジェクト])
Visual Basic プロジェクトのオプションに対する既定の設定を指定します。 新しいプロジェクトを作成すると、指定したオプション ステートメントがコード エディターのプロジェクト ヘッダーに追加されます。 このオプションは、すべての Visual Basic プロジェクトに適用されます。

このダイアログ ボックスにアクセスするには、**[ツール]** メニューの **[オプション]** をクリックし、**[プロジェクトおよびソリューション]** フォルダーを展開して、**[Visual Basic の既定値]** をクリックします。

 **Option Explicit**

明示的な変数の宣言が必要となるように、コンパイラの既定値を設定します。 既定では、**[Option Explicit]** は **[On]** に設定されています。 詳細については、「[/optionexplicit](/dotnet/visual-basic/reference/command-line-compiler/optionexplicit)」を参照してください。

 **Option Strict**

明示的な縮小変換を必要とし、遅延バインディングが許可されるように、コンパイラの既定値を設定します。 既定では、**[Option Strict]** は **[Off]** に設定されています。 詳細については、「[/optionstrict](/dotnet/visual-basic/reference/command-line-compiler/optionstrict)」を参照してください。

 **Option Compare**

文字列比較でのコンパイラの既定値を設定します。[binary] (大文字と小文字を区別する) または [text] (大文字と小文字を区別しない) を設定できます。既定では、 **[Option Compare]** は **[Binary]** に設定されています。 詳細については、「[/optioncompare](/dotnet/visual-basic/reference/command-line-compiler/optioncompare)」を参照してください。

 **Option Infer**

ローカル型の推論についてのコンパイラの既定値を設定します。 既定では、新しく作成されたプロジェクトの場合は **[Option Infer]** が **[On]** に設定され、以前のバージョンの Visual Basic で作成されて移行されたプロジェクトの場合は **[Off]** に設定されます。 詳細については、「[/optioninfer](/dotnet/visual-basic/reference/command-line-compiler/optioninfer)」を参照してください。

## <a name="see-also"></a>関連項目

- [ソリューションおよびプロジェクト](../../ide/solutions-and-projects-in-visual-studio.md)
