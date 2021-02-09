---
title: '方法: リボンに [開発] タブを表示する'
description: Visual Studio を使用して、Microsoft Word 文書のリボンに [開発者] タブをプログラムで表示する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 08/14/2019
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Ribbon [Office development in Visual Studio], tabs
- Developer tab [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 081d6740aa31a31173b12e467b1b8e32a074604a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99927718"
---
# <a name="how-to-show-the-developer-tab-on-the-ribbon"></a>方法: リボンに [開発] タブを表示する
  Office アプリケーションのリボンにある [ **開発者** ] タブにアクセスするには、既定では表示されないため、このタブを表示するように構成する必要があります。 たとえば、Word のドキュメント レベルのカスタマイズに <xref:Microsoft.Office.Tools.Word.GroupContentControl> を追加しようとする場合、このタブを表示する必要があります。

> [!NOTE]
> このガイダンスは Office 2010 以降のアプリケーションのみに適用されます。 2007 Microsoft Office システムにこのタブを表示する場合は、このトピックの次のバージョンを参照してください。 [方法: リボンに [開発者] タブを表示](https://web.archive.org/web/20140303033431/msdn.microsoft.com/library/bb608625(v=vs.90).aspx
)する」を参照してください。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

> [!NOTE]
> アクセスに [ **開発者** ] タブがありません。

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="to-show-the-developer-tab"></a>[開発] タブを表示するには

1. このトピックでサポートされている Office アプリケーションのいずれかを起動します。 このトピックの「 **適用先:** メモ」を参照してください。

2. [ **ファイル** ] タブで、[ **オプション** ] をクリックします。

     次の図は、Office 2010 の [ **ファイル** ] タブと [ **オプション** ] ボタンを示しています。

     ![Outlook 2010 で [ファイル]、[オプション] を選択](../vsto/media/vsto-office-file-tab.png "Outlook 2010 で [ファイル]、[オプション] を選択")

     次の図は、Office 2013 の [ **ファイル** ] タブを示しています。

     ![Outlook 2013 の [File] (ファイル) タブ](../vsto/media/vsto-office2013-filetab.png "Outlook 2013 の [File] (ファイル) タブ")

     次の図は、Office 2013 の [ **オプション** ] ボタンを示しています。

     ![Outlook 2013 Preview の [Options] (オプション) ボタン](../vsto/media/vsto-office2013-optionsbutton.png "Outlook 2013 Preview の [Options] (オプション) ボタン")

3. [ _ApplicationName_ の **オプション**] ダイアログボックスで、[**リボンのカスタマイズ**] ボタンをクリックします。

     次の図は、Excel 2010 の [ **オプション** ] ダイアログボックスと [ **リボンのカスタマイズ** ] ボタンを示しています。 このボタンの位置は、このトピックの上部付近の「対象」セクションに記載されている他のすべてのアプリケーションで同様です。

     ![[リボンのユーザー設定] ボタン](../vsto/media/vsto-office2010-customizeribbonbutton.png "[リボンのユーザー設定] ボタン")

4. メインタブの一覧で、[ **開発者** ] チェックボックスをオンにします。

     次の図は、Word 2010 およびの [ **開発者** ] チェックボックスを示して [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] います。 このチェック ボックスの位置は、このトピックの上部付近の「対象」セクションに記載されている他のすべてのアプリケーションと同様です。

     ![[Word のオプション] ダイアログの [開発] チェック ボックス](../vsto/media/vsto-office2010-developercheckbox.png "[Word のオプション] ダイアログの [開発] チェック ボックス")

5. **[OK** ] をクリックして、[**オプション**] ダイアログボックスを閉じます。

## <a name="see-also"></a>関連項目
- [Office UI のカスタマイズ](../vsto/office-ui-customization.md)
