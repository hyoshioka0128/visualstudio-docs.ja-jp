---
title: SharePoint 機能の作成 |Microsoft Docs
description: SharePoint フィーチャーを作成して、配置を簡単にするために関連する SharePoint プロジェクトアイテムをグループ化します。 SharePoint ソリューションに機能を追加します。 機能デザイナーを使用します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, features
- features [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 06a8fdef9c194e9b0f81768f93b675ade77d39ef
ms.sourcegitcommit: ad2c820b280b523a7f7aef89742cdb719354748f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94850586"
---
# <a name="create-sharepoint-features"></a>SharePoint 機能の作成
  SharePoint 機能を使用すると、関連する SharePoint プロジェクト項目をグループ化して、配置を簡単にすることができます。 SharePoint フィーチャーデザイナーを使用して、機能を作成し、スコープを設定し、他の機能を依存関係としてマークできます。 また、デザイナーはマニフェストも生成します。マニフェストは、各機能を記述する XML ファイルです。

## <a name="add-features-to-the-sharepoint-solution"></a>SharePoint ソリューションへの機能の追加
 SharePoint ソリューションに機能を追加するには、ソリューションエクスプローラーまたはパッケージングエクスプローラーを使用します。 機能を追加するには、次のいずれかの方法を使用できます。

- **ソリューションエクスプローラー** で、[**機能**] のショートカットメニューを開き、[**機能の追加**] を選択します。

- **パッケージングエクスプローラー** で、パッケージのショートカットメニューを開き、[機能の **追加**] を選択します。

## <a name="using-the-feature-designer"></a>機能デザイナーの使用
 SharePoint ソリューションには、ソリューションエクスプローラーの機能ノードの下にグループ化された1つ以上の SharePoint 機能を含めることができます。 各機能には、機能のプロパティをカスタマイズするために使用できる独自の **フィーチャーデザイナー** があります。 詳細については、「[方法:SharePoint フィーチャーをカスタマイズする](../sharepoint/how-to-customize-a-sharepoint-feature.md)」を参照してください。 機能を相互に区別するには、タイトル、説明、バージョン、スコープなどの機能のプロパティを構成します。

### <a name="feature-designer-options"></a>フィーチャーデザイナーのオプション
 フィーチャーを作成した後は、フィーチャーデザイナーを使用してカスタマイズできます。

 フィーチャーデザイナーに表示される機能のプロパティを次の表に示します。

|プロパティ|説明|
|--------------|-----------------|
|タイトル|省略可能。 この機能の既定のタイトルは、 *SolutionName* *FeatureName* に設定されています。|
|説明|省略可能。 SharePoint 機能の説明です。|
|Scope|必須。 **ソリューションエクスプローラー** を使用して機能を作成した場合、既定ではスコープは Web に設定されます。<br /><br /> -ファーム: サーバーファーム全体に対して機能をアクティブ化します。<br /><br /> -サイト: サイトコレクション内のすべての web サイトの機能をアクティブ化します。<br /><br /> -Web: 特定の web サイトの機能をアクティブ化します。<br /><br /> -WebApplication: web アプリケーション内のすべての web サイトの機能をアクティブにします。|
|[ソリューション内の項目]|フィーチャーに追加できるすべての SharePoint アイテム。|
|機能の項目|フィーチャーに追加された SharePoint プロジェクトアイテム。|

## <a name="add-and-remove-sharepoint-project-items"></a>SharePoint プロジェクト項目の追加と削除
 配置のために SharePoint 機能を追加する SharePoint プロジェクトアイテムを選択できます。 フィーチャー **デザイナー** を使用して、フィーチャーの項目を追加および削除したり、フィーチャーマニフェストを表示したりします。 詳細については、「 [方法: SharePoint 機能に項目を追加および削除](../sharepoint/how-to-add-and-remove-items-to-sharepoint-features.md)する」を参照してください。

## <a name="add-feature-dependencies"></a>機能の依存関係の追加
 フィーチャーマニフェストを構成すると、機能をアクティブ化する前に SharePoint サーバーが特定の機能をアクティブにすることができます。 たとえば、SharePoint 機能が機能またはデータの他の機能に依存している場合、SharePoint サーバーはまず、機能が依存しているすべての機能のアクティブ化を試みることができます。 詳細については、「 [方法: 機能の依存関係を追加および削除](../sharepoint/how-to-add-and-remove-feature-dependencies.md)する」を参照してください。

## <a name="see-also"></a>関連項目
- [方法: SharePoint 機能をカスタマイズする](../sharepoint/how-to-customize-a-sharepoint-feature.md)
- [方法: SharePoint 機能に項目を追加および削除する](../sharepoint/how-to-add-and-remove-items-to-sharepoint-features.md)
- [方法: フィーチャーの依存関係を追加および削除する](../sharepoint/how-to-add-and-remove-feature-dependencies.md)
