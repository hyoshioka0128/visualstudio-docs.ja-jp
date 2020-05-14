---
title: Visual Studio コマンドの GUID と ID |マイクロソフトドキュメント
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
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8932f23d301eabc97414bf76453d70336e0dabae
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708255"
---
# <a name="guids-and-ids-of-visual-studio-commands"></a>Visual Studio コマンドの GUID と ID
Visual Studio 統合開発環境 (IDE) に含まれるコマンドの GUID と ID の値は、Visual Studio SDK の一部としてインストールされる .vsct ファイルで定義されます。 詳細については[、「IDE で定義されたコマンド、メニュー、およびグループ](../../extensibility/internals/ide-defined-commands-menus-and-groups.md)」を参照してください。

 *vsct*ファイルで定義されている IDE オブジェクトを操作する方法の詳細については、「[メニューとコマンドを拡張](../../extensibility/extending-menus-and-commands.md)する」を参照してください。

## <a name="find-a-command-definition"></a>コマンド定義の検索
 Visual Studio では 1000 を超えるコマンドが定義されているため、これらをすべてここに表示することは現実的ではありません。 代わりに、コマンドの定義を見つけるためにこれらの手順に従います。

### <a name="to-locate-a-command-definition"></a>コマンド定義を検索するには

1. Visual Studio*Venusmenu.vsct*で *、<Visual Studio SDK のインストール\>パス \VisualStudioIntegration\Common\Inc\\*フォルダーで次のファイル*ShellCmdDef.vsct**を*開*きます。*

    ほとんどの Visual Studio コマンドは、*次*の例で定義*されています。* *VsDbgCmdUsed.vsct*はデバッガーに関連するコマンドを定義し *、Venusmenu.vsct*は Web 開発に固有のコマンドを定義します。

2. コマンドがメニュー項目の場合は、メニュー項目の正確なテキストをメモします。 コマンドがツールバーのボタンである場合は、一時停止したときに表示されるツールヒントテキストをメモします。

3. **Ctrl F キー**+**F**を押して **[検索**] ダイアログ ボックスを開きます。

4. [**検索する文字列**] ボックスに、手順 2 でメモしたテキストを入力します。

5. [ファイルの場所 **]** ボックスに **[開いているドキュメントすべて**] が表示されていることを確認します。

6. [Button 要素](../../extensibility/button-element.md)の`<Strings>`セクションでテキストが選択されるまで、[**次を検索**] ボタンをクリックします。

    コマンド`<Button>`が表示される要素は、コマンド定義です。

   コマンド定義が見つかったら、コマンドと同じ値と`guid``id`同じ値を持つ[CommandPlacement 要素](../../extensibility/commandplacement-element.md)を作成することで、コマンドのコピーを別のメニューまたはツールバーに配置できます。 詳細については、「[ボタンの再利用可能なグループを作成する](../../extensibility/creating-reusable-groups-of-buttons.md)」を参照してください。

### <a name="special-cases"></a>特殊なケース
 次の場合、メニュー テキストまたはツールヒントテキストがコマンド定義の内容と正確に一致しない場合があります。

- *P*に下線が付いている [**ファイル]** メニューの **[印刷**] コマンドなど、下線付きの文字を含むメニュー項目。

     メニュー項目名のアンパサンド (&) 文字の前に付いている文字は、下線付きで表示されます。 ただし *、.vsct*ファイルは、特殊文字を示すためにアンパサンド (&) 文字を使用し、アンパサンドを表示する必要がある XML*&amp;で*書き込まれます。 したがって *、.vsct*ファイルでは、**印刷**コマンドは*&amp;amp として表示されます。印刷*します。

- [現在のファイル名**を保存]**\<などの動的\>テキストを含むコマンド、**および [最近使ったファイル]** リストの項目など、動的に生成されたメニュー項目。

     ダイナミック テキストを検索する信頼できる方法はありません。 代わりに[、Visual Studio のメニューの GUID と ID、](../../extensibility/internals/guids-and-ids-of-visual-studio-menus.md)または Visual Studio ツール[バー](../../extensibility/internals/guids-and-ids-of-visual-studio-toolbars.md)の GUID と ID を参照して、目的のコマンドをホストするグループを見つけ、そのグループの ID を検索します。 コマンド定義が[親要素](../../extensibility/parent-element.md)としてグループを持たない場合は、コマンドの親を設定`<CommandPlacement>`する要素を*SearchSharedCmdPlace.vsct*および*ShellCmdPlace.vsct* (デバッガー コマンドの*VsDbgCmdPlace.vsct)* を検索します。 *フォルダー**フォルダーフォルダーフォルダー*内のフォルダー*ShellCmdPlace.vsct*フォルダーフォルダーフォルダーです。 * \<\>\\ *

## <a name="see-also"></a>関連項目

- [Visual Studio コマンド テーブル (.vsct) ファイル](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [VSCT XML スキーマ リファレンス](../../extensibility/vsct-xml-schema-reference.md)
