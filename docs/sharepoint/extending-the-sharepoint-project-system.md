---
title: SharePoint プロジェクトシステムの拡張 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, extending projects
- SharePoint development in Visual Studio, extending project items
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 7dce10c2bc44eb4fde6a6e38417d136ea5e9ba41
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62557025"
---
# <a name="extend-the-sharepoint-project-system"></a>SharePoint プロジェクトシステムの拡張
  SharePoint ソリューションを作成するには、Visual Studio で一連のプロジェクトテンプレートと項目テンプレートを使用します。 これらのテンプレートは、多くの開発シナリオの要件を満たしていますが、必要な機能が提供されない場合もあります。 このような場合は、SharePoint プロジェクトシステムを拡張できます。

## <a name="overview-of-the-sharepoint-project-system"></a>SharePoint プロジェクトシステムの概要
 SharePoint プロジェクトシステムは、 *sharepoint プロジェクトアイテム*の基本コンポーネントに基づいています。 SharePoint プロジェクトアイテムは、リスト定義、Web パーツ、コンテンツタイプなど、単一の SharePoint カスタマイズを表します。

 SharePoint プロジェクトは、1つまたは複数の SharePoint プロジェクトアイテムを含む Visual Studio プロジェクトです。 SharePoint プロジェクトには、配置のためにプロジェクト項目を機能やパッケージにグループ化する方法を定義する追加コンポーネントも含まれています。

 SharePoint プロジェクト項目と SharePoint プロジェクトの内容の詳細については、「 [sharepoint プロジェクト項目の項目テンプレートとプロジェクトテンプレートを作成](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)する」を参照してください。

## <a name="how-to-extend-the-sharepoint-project-system"></a>SharePoint プロジェクトシステムを拡張する方法
 SharePoint プロジェクトシステムは、次の方法で拡張できます。

- 独自の SharePoint プロジェクト項目の種類を定義し、Visual Studio の新しい項目テンプレートまたはプロジェクトテンプレートに関連付けます。 たとえば、カスタムアクションまたはフィールドを作成するために、SharePoint プロジェクトアイテムの種類を定義できます。 詳細については、「 [カスタム SharePoint プロジェクト項目の種類の定義](../sharepoint/defining-custom-sharepoint-project-item-types.md)」を参照してください。

- Visual Studio に既にインストールされている SharePoint プロジェクト項目の種類を拡張します。 たとえば、 **ソリューションエクスプローラー** のプロジェクト項目にショートカットメニュー項目を追加し、開発者がメニュー項目を選択したときにプロジェクト項目をカスタマイズできます。 詳細については、「 [SharePoint プロジェクト項目の拡張](../sharepoint/extending-sharepoint-project-items.md)」を参照してください。

- SharePoint プロジェクトを拡張します。 たとえば、SharePoint プロジェクトで項目が追加または削除されたときに、特定のタスクを実行するためのイベントハンドラーを追加できます。 詳細については、「 [SharePoint プロジェクトの拡張](../sharepoint/extending-sharepoint-projects.md)」を参照してください。

- SharePoint プロジェクト項目と SharePoint プロジェクトのパッケージ化と配置の動作を拡張します。 たとえば、プロジェクトを配置または取り消すときに実行する独自の配置手順を作成できます。また、Visual Studio で特定の配置手順を実行するときに、追加のカスタムタスクを実行することもできます。 詳細については、「 [SharePoint のパッケージ化と配置の拡張](../sharepoint/extending-sharepoint-packaging-and-deployment.md)」を参照してください。

## <a name="common-development-tasks"></a>一般的な開発タスク
 SharePoint プロジェクトシステムの拡張機能では、次の一般的なタスクを実行できます。

- プロジェクト項目およびさまざまな種類のプロジェクトファイルにカスタム文字列データを保存します。 詳細については、「 [SharePoint プロジェクトシステムの拡張機能にデータを保存](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)する」を参照してください。

- SharePoint プロジェクトシステムのオブジェクトを、Visual Studio オートメーションオブジェクトモデルまたは統合オブジェクトモデルの対応するオブジェクトに変換します。または、その逆も可能です。 詳細については、「 [SharePoint プロジェクトシステムの種類とその他の Visual Studio プロジェクトの種類の間の Conver](../sharepoint/converting-between-sharepoint-project-system-types-and-other-visual-studio-project-types.md)」を参照してください。

## <a name="see-also"></a>こちらもご覧ください
- [カスタム SharePoint プロジェクト項目の種類を定義する](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [SharePoint プロジェクト項目の拡張](../sharepoint/extending-sharepoint-project-items.md)
- [SharePoint プロジェクトの拡張](../sharepoint/extending-sharepoint-projects.md)
- [SharePoint のパッケージ化と配置の拡張](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
- [SharePoint プロジェクトシステムの拡張機能にデータを保存する](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)
- [SharePoint プロジェクトシステムの種類とその他の Visual Studio プロジェクトの種類の変換](../sharepoint/converting-between-sharepoint-project-system-types-and-other-visual-studio-project-types.md)
- [Visual Studio での SharePoint ツールの拡張](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)
- [SharePoint ツール拡張機能におけるプログラミングに関する概念および特徴](../sharepoint/programming-concepts-and-features-for-sharepoint-tools-extensions.md)
