---
title: N 層アプリケーションでのデータセットの操作 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- datasets [Visual Basic], n-tier applications
- multi-tier database applications
- DataSet project [VS n-tier applications]
- distributed applications [VS n-tier applications]
- data [Visual Basic], n-tier applications
- TableAdapters, n-tier applications
- n-tier applications
- tiers, n-tier applications
- typed datasets, n-tier applications
- multiple tier applications
ms.assetid: f6ae2ee0-ea5f-4a79-8f4b-e21c115afb20
caps.latest.revision: 25
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 4f7be307ec94b15871da20ace8055fc7121d5d92
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72657810"
---
# <a name="work-with-datasets-in-n-tier-applications"></a>n 層アプリケーションでのデータセットの操作
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

N 層データアプリケーション * は、複数の論理層 (または *層*) に分割されるデータ中心のアプリケーションです。 言い換えれば、n 層データ アプリケーションは、複数のプロジェクトに分離されたアプリケーションであり、データ アクセス層、ビジネス ロジック層、およびプレゼンテーション層がそれぞれ独自のプロジェクトに含まれています。 詳細については、「 [N 層データアプリケーションの概要](../data-tools/n-tier-data-applications-overview.md)」を参照してください。

 TableAdapter およびデータセット クラスを別々のプロジェクトに生成できるように、型指定されたデータセットが強化されました。 これにより、アプリケーション層を分離して、n 層データ アプリケーションをすばやく生成できます。

 型指定されたデータセットで n 層をサポートすることで、アプリケーションアーキテクチャを n 層設計に反復的に開発できます。また、コードを複数のプロジェクトに手動で分離する必要もなくなります。 データセットデザイナーを使用したデータレイヤーのデザインを開始します。 アプリケーション アーキテクチャを n 層デザインにする準備ができたら、データセット クラスが別個のプロジェクトに生成されるようにデータセットの **[DataSet プロジェクト]** プロパティを設定します。

## <a name="in-this-section"></a>このセクションの内容
 [データセットと tableadapter を別々のプロジェクトに分離](../data-tools/separate-datasets-and-tableadapters-into-different-projects.md) する生成されたデータセットクラスを、生成された TableAdapter クラスを含むプロジェクトから新しいプロジェクトに移動する方法について説明します。

 [N 層アプリケーションの tableadapter にコードを追加](../data-tools/add-code-to-tableadapters-in-n-tier-applications.md) するN 層 TableAdapter のコードを追加できる部分クラスを生成する方法について説明します。

 [N 層アプリケーションのデータセットにコードを追加する](../data-tools/add-code-to-datasets-in-n-tier-applications.md) N 層データセットのコードを追加できる部分クラスを生成する方法について説明します。

 [N 層データセットに検証を追加する](../data-tools/add-validation-to-an-n-tier-dataset.md) データの変更時に検証を実行するコードを追加する場所について説明します。

 [チュートリアル: N 層データアプリケーションの作成](../data-tools/walkthrough-creating-an-n-tier-data-application.md) 型指定されたデータセットを作成し、TableAdapter とデータセットコードを複数のプロジェクトに分割する手順について説明します。

 [チュートリアル: N 層データアプリケーションへの検証の追加](https://msdn.microsoft.com/library/b35d072c-31f0-49ba-a225-69177592c265) N 層データアプリケーションのチュートリアルで作成したアプリケーションに検証を追加する手順について説明します。

## <a name="reference"></a>関連項目
 <xref:System.Data.DataSet>

 <xref:System.Data.TypedTableBase%601>

## <a name="related-sections"></a>関連項目

- [N 層データアプリケーションの概要](../data-tools/n-tier-data-applications-overview.md)
- [階層更新](../data-tools/hierarchical-update.md)
- [Visual Studio のデータセットツール](../data-tools/dataset-tools-in-visual-studio.md)
- [Visual Studio でのデータへのアクセス](../data-tools/accessing-data-in-visual-studio.md)
- [LINQ to SQL を使用する n 層アプリケーションとリモート アプリケーション](https://msdn.microsoft.com/library/854a1cdd-53cb-45f5-83ca-63962a9b3598)