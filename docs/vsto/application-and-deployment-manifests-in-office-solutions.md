---
title: Office ソリューションのアプリケーションマニフェストと配置マニフェスト
description: アプリケーションマニフェストは、Office ソリューションがアセンブリを検索および更新するために使用する情報を提供する XML ファイルです。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- manifests [Office development in Visual Studio]
- deployment manifests [Office development in Visual Studio]
- application manifests [Office development in Visual Studio]
- assemblies [Office development in Visual Studio], updating
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 9ca8cf2774b7a24ec3bef40418b6a2157bf0f992
ms.sourcegitcommit: ce85cff795df29e2bd773b4346cd718dccda5337
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/08/2020
ms.locfileid: "96844713"
---
# <a name="application-and-deployment-manifests-in-office-solutions"></a>Office ソリューションのアプリケーションマニフェストと配置マニフェスト
  アプリケーション マニフェストは、Office ソリューションがアセンブリを特定して更新する際に使用する情報を提供する XML ファイルです。 アプリケーション マニフェストは配置マニフェストと共に使用できます。配置マニフェストは、サーバーに保存されている XML ファイルです。最新バージョンのアプリケーション マニフェストとアセンブリを特定するために必要な情報を提供します。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="manifest-structure-for-office-solutions"></a>Office ソリューションのマニフェストの構造
 Visual Studio で Office 開発ツールを使用して作成された Microsoft Office ソリューションの場合、すべてのマニフェストは、標準の ClickOnce スキーマに基づいています。 Office ソリューションを配置すると、ドキュメントレベルと VSTO アドイン プロジェクトの両方のアプリケーション マニフェストは、ClickOnce キャッシュに保存されます。 配置マニフェストは、クライアント コンピューターにコピーされません。

 Office プロジェクトのアプリケーションマニフェストと配置マニフェストの内容については、「office [ソリューションのアプリケーションマニフェスト](../vsto/application-manifests-for-office-solutions.md) 」と「 [Office ソリューションの配置マニフェスト](../vsto/deployment-manifests-for-office-solutions.md)」を参照してください。

## <a name="create-application-and-deployment-manifests"></a>アプリケーションマニフェストと配置マニフェストの作成
 アプリケーション マニフェストは、ビルド プロセスの一環として自動的に作成されます。 ドキュメントレベルのプロジェクトをビルドするたびに、配置マニフェストの場所はカスタム ドキュメント プロパティとしてドキュメントに埋め込まれます。 VSTO アドインの場合、配置マニフェストの場所はレジストリに格納されます。

 **発行ウィザード** の詳細については、「 [ClickOnce を使用した Office ソリューションの配置](../vsto/deploying-an-office-solution-by-using-clickonce.md)」を参照してください。

 Office ソリューションでのマニフェストの動作の詳細については、「 [office ソリューションの配置](../vsto/deploying-an-office-solution.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [ドキュメントレベルのカスタマイズのアーキテクチャ](../vsto/architecture-of-document-level-customizations.md)
- [Architecture of VSTO Add-Ins](../vsto/architecture-of-vsto-add-ins.md)
- [Office ソリューションの設計と作成](../vsto/designing-and-creating-office-solutions.md)
- [Office ソリューション用アプリケーションマニフェスト](../vsto/application-manifests-for-office-solutions.md)
- [Office ソリューションの配置マニフェスト](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce アプリケーションマニフェスト](../deployment/clickonce-application-manifest.md)
- [ClickOnce 配置マニフェスト](../deployment/clickonce-deployment-manifest.md)