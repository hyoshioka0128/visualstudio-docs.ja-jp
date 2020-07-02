---
title: Office ソリューションの構成情報を設定する
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- solutions [Office development in Visual Studio], configuration files
- configuration files [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 8a0868019247e20b9154690469d4c291f1f8e0d6
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545809"
---
# <a name="how-to-set-up-configuration-information-for-an-office-solution"></a>方法: Office ソリューションの構成情報を設定する
  構成ファイルを使用すると、Office ソリューションに固有の設定を構成できます。 アセンブリバインディングポリシー、リモート処理オブジェクト、デバッグ、トレース設定などの設定を指定できます。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

### <a name="to-add-a-configuration-file-to-your-office-project"></a>Office プロジェクトに構成ファイルを追加するには

1. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

2. [**カテゴリ**] ペインで、[**全般**] をクリックします。

3. [**テンプレート**] ペインで、[**アプリケーション構成ファイル**] を選択します。

4. [**名前**] ボックスに、アセンブリと拡張子 *.config*を加えた名前を入力します。たとえば、 *ExcelWorkbook1.dll*という名前の Excel プロジェクトアセンブリの構成ファイルに*ExcelWorkbook1.dll.config*という名前が付けられます。

5. **[追加]** をクリックします。

6. アプリケーション構成ファイルのスキーマに従って、構成ファイルを作成します。 詳細については、「 [.NET Framework の構成ファイルスキーマ](/dotnet/framework/configure-apps/file-schema/index)」を参照してください。

   Office プロジェクトで構成ファイルを使用する場合、特別な考慮事項はありません。

## <a name="see-also"></a>関連項目
- [.NET Framework の構成ファイルスキーマ](/dotnet/framework/configure-apps/file-schema/index)
- [Office ソリューションの設計と作成](../vsto/designing-and-creating-office-solutions.md)
- [Office ソリューションの配置](../vsto/deploying-an-office-solution.md)
