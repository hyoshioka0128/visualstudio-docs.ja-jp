---
title: Visual Basic の IntelliSense
description: Visual Basic ソース コード エディターによって提供される IntelliSense 機能を使用する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.Basic.IntelliSense
helpviewer_keywords:
- IntelliSense [Visual Basic]
- IntelliSense [Visual Studio], Visual Basic
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 70cdcf9eb6d741fc579ce555ce0bfa3cdea0d774
ms.sourcegitcommit: df6ba39a62eae387e29f89388be9e3ee5ceff69c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2020
ms.locfileid: "96478823"
---
# <a name="intellisense-for-visual-basic-code-files"></a>Visual Basic コード ファイルの IntelliSense

Visual Basic ソース コード エディターでは、次の IntelliSense 機能が提供されます。

## <a name="syntax-tips"></a>構文のヒント

構文のヒントには、入力中のステートメントの構文が表示されます。 これは、[Declare](/dotnet/visual-basic/language-reference/statements/declare-statement) などのステートメントで役立ちます。

## <a name="automatic-completion"></a>自動補完

- さまざまなキーワードの補完

     たとえば、`goto` とスペースを入力した場合、IntelliSense ではドロップダウン メニューに定義されたラベルのリストが表示されます。 その他のサポートされているキーワードには、`Exit`、`Implements`、`Option`、および `Declare` が含まれます。

- `Enum` および `Boolean` での補完

    ステートメントが列挙型のメンバーを参照する場合、IntelliSense では `Enum` のメンバーのリストが表示されます。 ステートメントが `Boolean` を参照する場合、IntelliSense では true-false ドロップダウン メニューが表示されます。

既定で補完機能を無効にするには、**[Visual Basic]** フォルダーの **[全般]** プロパティ ページで、**[自動メンバー表示]** の選択を解除します。

[メンバーの一覧] または [入力候補] を呼び出すか、**Alt**+**→** キーを押して、補完機能を手動で起動することができます。 詳細については、[IntelliSense の使用](../ide/using-intellisense.md)に関するページを参照してください。

## <a name="intellisense-in-zone"></a>ゾーン内の IntelliSense

ゾーン内の IntelliSense は、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] を使用してアプリケーションを配置する必要があり、部分信頼設定に制限された Visual Basic 開発者を支援します。 この機能を使用すると、次のことが可能になります。

- アプリケーションを実行するアクセス許可を選択する。

- [メンバーの一覧] で選択したゾーンの API を使用可能なものとして表示し、追加のアクセス許可が必要な API を使用できないものとして表示する。

詳細については、「[ClickOnce アプリケーションのコード アクセス セキュリティ](../deployment/code-access-security-for-clickonce-applications.md)」を参照してください。

## <a name="filtered-completion-lists"></a>フィルター処理されたコンプリート リスト

Visual Basic の IntelliSense コンプリート リストには、リストの下部近くに 2 つのタブ コントロールがあります。 既定で選択されている **[よく使われる候補]** タブには、作成しているステートメントを完成するために最もよく使われる項目が表示されます。 **[すべて]** タブには、**[よく使われる候補]** タブに表示されている項目も含めて、オート コンプリートで使用可能なすべての項目が表示されます。

## <a name="see-also"></a>関連項目

- [IntelliSense を使用する](../ide/using-intellisense.md)
