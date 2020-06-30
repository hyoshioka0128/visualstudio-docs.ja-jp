---
title: '方法: Office 多言語ユーザーインターフェイスを対象にする'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- globalization [Office development in Visual Studio], user interface targeting
- MUI [Office development in Visual Studio]
- Office applications [Office development in Visual Studio], localization
- Multilingual User Interface [Office development in Visual Studio]
- localization [Office development in Visual Studio], user interface targeting
- Office applications [Office development in Visual Studio], globalization
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 5217f2d6cf67eced00c0c84b9bacda94573c5a09
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85537502"
---
# <a name="how-to-target-the-office-multilingual-user-interface"></a>方法: Office 多言語ユーザーインターフェイスを対象にする
  多言語ユーザーインターフェイス (MUI) は、エンドユーザーがユーザーインターフェイス (UI) の言語を変更できるようにする Microsoft Office の機能です。 たとえば、英語の UI を使用するエンドユーザーは、UI の言語をスペイン語に変更できます。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 多くの言語の Office を使用しているユーザーがアプリケーションを使用する場合は、ユーザーのコンピューターで Office で使用されている言語に合わせて UI 文字列の言語を自動的に変更するコードを追加できます (ユーザーが適切なリソースをインストールしている場合)。

## <a name="to-check-the-current-office-ui-setting"></a>現在の Office UI 設定を確認するには

1. <xref:System.Threading.Thread.CurrentUICulture%2A>現在のスレッドのプロパティを使用します。 ユーザーのコンピューターで現在実行されている Office のバージョンで使用される言語に合わせて、UI 文字列の言語を設定します。

     [!code-vb[Trin_VstcoreCreatingExcel#10](../vsto/codesnippet/VisualBasic/Trin_VstcoreCreatingExcelVB/Sheet1.vb#10)]
     [!code-csharp[Trin_VstcoreCreatingExcel#10](../vsto/codesnippet/CSharp/Trin_VstcoreCreatingExcelCS/Sheet1.cs#10)]

## <a name="see-also"></a>関連項目
- [方法: プライマリ相互運用機能アセンブリを使用して Office アプリケーションを対象にする](../vsto/how-to-target-office-applications-through-primary-interop-assemblies.md)
- [Office ソリューションの遅延バインディング](../vsto/late-binding-in-office-solutions.md)
