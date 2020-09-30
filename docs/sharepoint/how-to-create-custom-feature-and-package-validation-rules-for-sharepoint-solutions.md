---
title: SharePoint ソリューションの機能とパッケージの検証を作成する
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, extending deployment
- SharePoint development in Visual Studio, validation rules
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 7ac718d16383448ea13f01ad367d97f917bb42ed
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "91585824"
---
# <a name="create-feature-and-package-validations-for-sharepoint-solutions"></a>SharePoint ソリューションの機能とパッケージの検証を作成する

  カスタム検証規則を作成して、Visual Studio によって生成されたソリューションパッケージを確認できます。 機能またはパッケージ全体に対して完全な検証を実行するに**は、パッケージ**または機能のコンテキストメニューの [**検証**] を選択します。 部分検証は、新しい SharePoint プロジェクト項目またはフィーチャーをプロジェクトに追加して、パッケージまたは機能が有効な状態であるかどうかを判断するときに実行されます。

### <a name="to-create-a-custom-package-validation-rule"></a>カスタムパッケージ検証規則を作成するには

1. クラス ライブラリ プロジェクトを作成します。

2. 次のアセンブリへの参照を追加します。

    - Microsoft.VisualStudio.SharePoint

    - System.ComponentModel.Composition

3. 次のいずれかのインターフェイスを実装するクラスを作成します。

    - パッケージ検証規則を作成するには、インターフェイスを実装し <xref:Microsoft.VisualStudio.SharePoint.Validation.IPackageValidationRule> ます。

    - フィーチャー検証規則を作成するには、インターフェイスを実装し <xref:Microsoft.VisualStudio.SharePoint.Validation.IFeatureValidationRule> ます。

4. <xref:System.ComponentModel.Composition.ExportAttribute>をクラスに追加します。 この属性を使用すると、Visual Studio で検証規則を検出して読み込むことができます。 <xref:Microsoft.VisualStudio.SharePoint.Validation.IPackageValidationRule>または <xref:Microsoft.VisualStudio.SharePoint.Validation.IFeatureValidationRule> 型を属性コンストラクターに渡します。

## <a name="example"></a>例
 次のコード例は、カスタムフィーチャー検証規則を作成する方法を示しています。

 [!code-vb[SPExtensibility.FeatureValidation#1](../sharepoint/codesnippet/VisualBasic/featurevalidation/extension/customvalidationrule.vb#1)]
 [!code-csharp[SPExtensibility.FeatureValidation#1](../sharepoint/codesnippet/CSharp/featurevalidation/extension/customfeaturevalidationrule.cs#1)]

## <a name="compile-the-code"></a>コードのコンパイル
 この例では、次のアセンブリへの参照が必要です。

- VisualStudio。

- System.componentmodel。

## <a name="deploy-the-extension"></a>拡張機能のデプロイ
 拡張機能を配置するには、 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] アセンブリおよび拡張機能と共に配布するその他のファイル用の拡張機能 (VSIX) パッケージを作成します。 詳細については、「 [Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [SharePoint のパッケージ化と配置の拡張](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
