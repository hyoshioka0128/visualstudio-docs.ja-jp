---
title: Visual Studio コマンドの Guid と Id |Microsoft Docs
description: Visual Studio 統合開発環境 (IDE) に含まれているコマンドの GUID と ID の値を見つける方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands
- id
- command placement
- visual studio command
- guid
ms.assetid: 2ea4bee2-0259-4675-8e65-2023b312b516
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: db0c417c40a2f2d02adef9c7a9e7274f95592015
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99898281"
---
# <a name="guids-and-ids-of-visual-studio-commands"></a>Visual Studio コマンドの Guid と Id
Visual Studio 統合開発環境 (IDE) に含まれるコマンドの GUID と ID の値は、Visual Studio SDK の一部としてインストールされる、vsct ファイルで定義されています。 詳細については、「 [IDE で定義されたコマンド、メニュー、およびグループ](../../extensibility/internals/ide-defined-commands-menus-and-groups.md)」を参照してください。

 *Vsct* ファイルで定義されている IDE オブジェクトを操作する方法の詳細については、「[メニューとコマンドの拡張](../../extensibility/extending-menus-and-commands.md)」を参照してください。

## <a name="find-a-command-definition"></a>コマンド定義の検索
 Visual Studio では、1000を超えるコマンドが定義されているため、ここですべてを一覧表示するのは現実的ではありません。 代わりに、次の手順に従ってコマンドの定義を検索します。

### <a name="to-locate-a-command-definition"></a>コマンド定義を検索するには

1. Visual Studio で、 *<Visual STUDIO SDK のインストールパス \> \VisualStudioIntegration\Common\Inc \\* フォルダーにある、 *sharedcmddef. vsct*、 *shellcmddef. vsct*、 *vsdbgcmdused.* vsct、の各ファイルを *開きます。*

    ほとんどの Visual Studio コマンドは、 *Sharedcmddef. vsct* および *shellcmddef. vsct* で定義されています。 *Vsdbgcmdused。 vsct* は、デバッガーに関連するコマンドと、[] を定義し *ます。 Vsct* は、Web 開発に固有のコマンドを定義します。

2. コマンドがメニュー項目の場合は、メニュー項目のテキストを正確に確認します。 コマンドがツールバーのボタンである場合は、一時停止したときに表示されるツールヒントのテキストを確認します。

3. **Ctrl** + **F** キーを押して [**検索**] ダイアログボックスを開きます。

4. [ **検索** する文字列] ボックスに、手順2でメモしたテキストを入力します。

5. すべての **開い** ているドキュメントが [ **検索対象** ] ボックスに表示されていることを確認します。

6. ボタン要素のセクションでテキストが選択されるまで、[**次を検索**] ボタンをクリックし `<Strings>` ます。 [](../../extensibility/button-element.md)

    `<Button>`コマンドが表示される要素は、コマンド定義です。

   コマンドの定義が見つかったら、コマンドと同じ値を持つ [Commandplacement 要素](../../extensibility/commandplacement-element.md) を作成することによって、別のメニューまたはツールバーにコマンドのコピーを配置でき `guid` `id` ます。 詳細については、「 [再利用可能なボタンのグループの作成](../../extensibility/creating-reusable-groups-of-buttons.md)」を参照してください。

### <a name="special-cases"></a>特殊なケース
 次の場合、メニューテキストまたはツールヒントのテキストが、コマンド定義の内容と正確に一致しない可能性があります。

- [**ファイル**] メニューの [**印刷**] コマンドなど、下線付きの文字を含むメニュー項目。 *P* は下線付きで表示されます。

     メニュー項目名のアンパサンド (&) 文字の前にある文字は、下線付きで表示されます。 ただし、 *vsct* ファイルは XML で記述されます。この XML では、アンパサンド (&) 文字を使用して特殊文字を指定し、表示するアンパサンドを *&amp; amp;* として指定する必要があります。 したがって、 *vsct* ファイルでは、 **Print** コマンドは *&amp; amp; として表示されます。印刷*。

- [**保存**] などの動的なテキストと、[最近使ったファイル] の一覧にある項目などの動的に \<Current Filename\> 生成されたメニュー項目を含むコマンド。

     動的テキストを検索するための信頼性の高い方法はありません。 代わりに、visual [studio のメニューの guid と id](../../extensibility/internals/guids-and-ids-of-visual-studio-menus.md) 、または [visual studio のツールバーの guid と](../../extensibility/internals/guids-and-ids-of-visual-studio-toolbars.md)id を参照して、目的のコマンドをホストするグループを検索し、そのグループの ID を検索します。 コマンド定義にグループが [親要素](../../extensibility/parent-element.md)として含まれていない場合は、コマンドの親を設定する要素に対して、 *sharedcmdplace. Vsct* および *shellcmdplace* (デバッガーコマンドの場合は *vsdbgcmdplace* ) を検索します。 `<CommandPlacement>` *Sharedcmdplace vsct*、 *shellcmdplace vsct*、および *vsdbgcmdplace* は *\<Visual Studio SDK installation path\> \VisualStudioIntegration\Common\Inc \\* フォルダーにあります。

## <a name="see-also"></a>関連項目

- [Visual Studio コマンドテーブル (vsct) ファイル](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [VSCT XML スキーマリファレンス](../../extensibility/vsct-xml-schema-reference.md)
