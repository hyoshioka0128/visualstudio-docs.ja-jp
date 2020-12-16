---
title: '方法: Office ソリューションに署名する'
description: 証明書を証拠として使用して、Microsoft Office ソリューションに信頼を付与する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- certificates [Office development in Visual Studio], Office solutions
- security [Office development in Visual Studio], signing Office solutions
- signing manifests [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 7451630570e6d557dc5d2b635d149ebc07cfb388
ms.sourcegitcommit: 4bd2b770e60965fc0843fc25318a7e1b46137875
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/15/2020
ms.locfileid: "97528114"
---
# <a name="how-to-sign-office-solutions"></a>方法: Office ソリューションに署名する
  ソリューションに署名する場合は、証明書を証拠として使用して、ソリューションに信頼を付与することができます。 複数のソリューションに同じ証明書を使用することができ、すべてのソリューションは、追加のセキュリティポリシーの更新なしで信頼されます。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 マニフェスト生成および編集ツール (*mage.exe* と *mageui.exe*) を使用してアプリケーションマニフェストと配置マニフェストを手動で編集する場合は、マニフェストを使用する前に再署名する必要があります。 詳細については、「 [方法: アプリケーションマニフェストおよび配置マニフェストに再署名](../deployment/how-to-re-sign-application-and-deployment-manifests.md)する」を参照してください。

## <a name="sign-by-using-a-certificate"></a>証明書を使用して署名する
 証明書は、一意のキーとソリューション発行者の id を含むファイルです。 証明機関から証明書を購入するか、独自の証明書を作成して証明機関に署名することができます。

 Visual Studio は、デバッグを有効にするために、一時的な証明書を使用して Office ソリューションに署名します。 デプロイされたソリューションの一時証明書を証拠として使用しないでください。

### <a name="to-sign-an-office-solution-by-using-a-certificate"></a>証明書を使用して Office ソリューションに署名するには

1. [**プロジェクト**] メニューの [ _SolutionName_ の **プロパティ**] をクリックします。

2. **[署名]** タブをクリックします。

3. [ **ClickOnce マニフェストに署名する**] を選択します。

4. [ **ストアから選択]** をクリックするか、 **[ファイルから** 選択] をクリックして証明書を探し、証明書に移動します。

5. 正しい証明書が使用されていることを確認するには **、[詳細] をクリック** して証明書の情報を表示します。

## <a name="see-also"></a>関連項目

- [セキュリティで保護された Office ソリューション](../vsto/securing-office-solutions.md)
- [Office ソリューションへの信頼の付与](../vsto/granting-trust-to-office-solutions.md)
- [[署名] ページ (プロジェクト デザイナー)](../ide/reference/signing-page-project-designer.md)
