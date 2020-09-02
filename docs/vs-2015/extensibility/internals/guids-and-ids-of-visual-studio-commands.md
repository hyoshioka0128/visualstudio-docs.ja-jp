---
title: コマンドの Guid と Id |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- commands
- id
- command placement
- visual studio command
- guid
ms.assetid: 2ea4bee2-0259-4675-8e65-2023b312b516
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2feef3cbe72b7eb8db96052236fe483733e22273
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62538139"
---
# <a name="guids-and-ids-of-visual-studio-commands"></a>Visual Studio コマンドの GUID および ID
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Visual Studio 統合開発環境 (IDE) に含まれるコマンドの GUID と ID の値は、Visual Studio SDK の一部としてインストールされる、vsct ファイルで定義されています。 詳細については、「 [IDE で定義されたコマンド、メニュー、およびグループ](../../extensibility/internals/ide-defined-commands-menus-and-groups.md)」を参照してください。

 Vsct ファイルで定義されている IDE オブジェクトを操作する方法の詳細については、「 [メニューとコマンドの拡張](../../extensibility/extending-menus-and-commands.md)」を参照してください。

## <a name="finding-a-command-definition"></a>コマンド定義の検索
 Visual Studio では、1000を超えるコマンドが定義されているため、ここですべてを一覧表示するのは現実的ではありません。 代わりに、次の手順に従ってコマンドの定義を検索します。

#### <a name="to-locate-a-command-definition"></a>コマンド定義を検索するには

1. Visual Studio で、 *Visual STUDIO SDK のインストールパス*\VisualStudioIntegration\Common\Inc\ フォルダーにある次のファイルを開きます。 Vsct、shellcmddef. Vsct、VsDbgCmdUsed。 vsct。 vsct。

    ほとんどの Visual Studio コマンドは、SharedCmdDef. vsct および ShellCmdDef. vsct で定義されています。 VsDbgCmdUsed。 vsct は、デバッガーに関連するコマンドと、[] を定義します。 vsct は、Web 開発に固有のコマンドを定義します。

2. コマンドがメニュー項目の場合は、メニュー項目のテキストを正確に確認します。 コマンドがツールバーのボタンである場合は、一時停止したときに表示されるツールヒントのテキストを確認します。

3. CTRL キーを押しながら F キーを押して、[ **検索** ] ダイアログボックスを開きます。

4. [ **検索** する文字列] ボックスに、手順2でメモしたテキストを入力します。

5. すべての **開い** ているドキュメントが [ **検索対象** ] ボックスに表示されていることを確認します。

6. ボタン要素のセクションでテキストが選択されるまで、[**次を検索**] ボタンをクリックし `<Strings>` ます。 [Button Element](../../extensibility/button-element.md)

    `<Button>`コマンドが表示される要素は、コマンド定義です。

   コマンドの定義が見つかったら、コマンドと同じ値を持つ [Commandplacement 要素](../../extensibility/commandplacement-element.md) を作成することによって、別のメニューまたはツールバーにコマンドのコピーを配置でき `guid` `id` ます。 詳細については、「 [再利用可能なボタンのグループの作成](../../extensibility/creating-reusable-groups-of-buttons.md)」を参照してください。

### <a name="special-cases"></a>特殊なケース
 次の場合、メニューテキストまたはツールヒントのテキストが、コマンド定義の内容と正確に一致しない可能性があります。

- [**ファイル**] メニューの [**印刷**] コマンドなど、下線付きの文字を含むメニュー項目。 P は下線付きで表示されます。

     メニュー項目名の "&" 文字の前にある文字は、下線付きで表示されます。 ただし、vsct ファイルは XML で記述されます。この XML では、' & ' 文字を使用して特殊文字を示し、表示するアンパサンドを ' ' として入力する必要があります。 &amp; したがって、vsct ファイルでは、 **print** コマンドは ' print ' として表示され &amp; ます。

- 現在のファイル*名*の**保存**、動的に生成されたメニュー項目など、動的なテキストを持つコマンド ([**最近使ったファイル**] の一覧の項目など)。

     動的テキストを検索するための信頼性の高い方法はありません。 代わりに、visual [studio のメニューの guid と id](../../extensibility/internals/guids-and-ids-of-visual-studio-menus.md) 、または [Visual Studio のツールバーの guid と](../../extensibility/internals/guids-and-ids-of-visual-studio-toolbars.md)id を参照して、目的のコマンドをホストするグループを検索し、そのグループの ID を検索します。 コマンド定義にグループが [親要素](../../extensibility/parent-element.md)として含まれていない場合は、 `<CommandPlacement>` コマンドの親を設定する要素に対して、sharedcmdplace. Vsct および shellcmdplace (デバッガーコマンドの場合は vsdbgcmdplace) を検索します。 SharedCmdPlace vsct、ShellCmdPlace vsct、andVsDbgCmdPlace は、 *Visual STUDIO SDK のインストールパス*\VisualStudioIntegration\Common\Inc\ フォルダーにあります。

## <a name="see-also"></a>参照
 [Menucommands と OleMenuCommands](../../misc/menucommands-vs-olemenucommands.md) [Visual Studio コマンドテーブル (.Vsct) ファイル](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md) [VSCT XML スキーマリファレンス](../../extensibility/vsct-xml-schema-reference.md)
