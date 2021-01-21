---
title: プロジェクト テンプレートと項目テンプレートのトラブルシューティング
description: テンプレートを開発環境に読み込むことができない場合に、テンプレートのトラブルシューティングを行う方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 01/02/2018
ms.topic: troubleshooting
helpviewer_keywords:
- templates [Visual Studio], troubleshooting
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: 42dc34d846f37ed1d7655d6758d045b2db7187d9
ms.sourcegitcommit: d6207a3a590c9ea84e3b25981d39933ad5f19ea3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/24/2020
ms.locfileid: "95596847"
---
# <a name="how-to-troubleshoot-templates"></a>方法: テンプレートの問題を解決する

テンプレートを開発環境に読み込むことができない場合に、問題を突き止める方法はいくつかあります。

## <a name="validate-the-vstemplate-file"></a>vstemplate ファイルを検証する

::: moniker range="vs-2017"

テンプレートの *vstemplate* ファイルが Visual Studio テンプレート スキーマに準拠していないと、テンプレートが **[新しいプロジェクト]** ダイアログ ボックスに表示されないことがあります。

::: moniker-end

::: moniker range=">=vs-2019"

テンプレート内の *vstemplate* ファイルが Visual Studio テンプレート スキーマに準拠していないと、新しいプロジェクトを作成する場合にテンプレートがダイアログ ボックスに表示されないことがあります。

::: moniker-end

### <a name="to-validate-the-vstemplate-file"></a>vstemplate ファイルを検証するには

1. テンプレートを含む *.zip* ファイルを探します。

1. *.zip* ファイルを展開します。

1. Visual Studio の **[ファイル]** メニューで、 **[開く]**  >  **[ファイル]** の順に選択します。

1. テンプレートの *vstemplate* ファイルを選択し、 **[開く]** を選択します。

1. *vstemplate* ファイルの XML がテンプレート スキーマに準拠していることを確認します。 *vstemplate* スキーマの詳細については、[テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)に関するページを参照してください。

    > [!NOTE]
    > *vstemplate* ファイルを作成する際に IntelliSense サポートを取得するには、`xmlns` 属性を `VSTemplate` 要素に追加し、 `http://schemas.microsoft.com/developer/vstemplate/2005` の値を割り当てます。

1. *vstemplate* ファイルを保存して、閉じます。

1. テンプレートに含まれるファイルを選択して右クリックし、 **[送る]**  >  **[圧縮 (zip 形式) フォルダー]** の順に選択します。 選択したファイルは *.zip* ファイルに圧縮されます。

1. 新しい *.zip* ファイルを古い *.zip* ファイルと同じディレクトリに配置します。

1. 抽出したテンプレート ファイルと古いテンプレート *.zip* ファイルを削除します。

## <a name="enable-diagnostic-logging"></a>診断ログの有効化

[テンプレートの検出のトラブルシューティング (機能拡張)](../extensibility/troubleshooting-template-discovery.md)に関するページの手順に従って、テンプレートの検出の診断ログを有効にできます。

## <a name="see-also"></a>参照

- [テンプレートの検出のトラブルシューティング (機能拡張)](../extensibility/troubleshooting-template-discovery.md)
- [テンプレートのカスタマイズ](../ide/customizing-project-and-item-templates.md)
- [プロジェクト テンプレートと項目テンプレートを作成する](../ide/creating-project-and-item-templates.md)
- [テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
