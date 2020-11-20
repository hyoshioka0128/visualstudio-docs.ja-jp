---
title: n 層アプリケーションでのデータセットの操作
description: N 層アプリケーションでのデータセットの操作方法について説明します。 N 層データアプリケーションは、複数の論理層 (または層) に分離されたデータ中心のアプリです。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
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
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: d450bb60bdb604f658f73d0b5df4b9bd739cf923
ms.sourcegitcommit: 72a49c10a872ab45ec6c6d7c4ac7521be84526ff
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2020
ms.locfileid: "94998188"
---
# <a name="work-with-datasets-in-n-tier-applications"></a>n 層アプリケーションでのデータセットの操作

*N 層データアプリケーション* は、複数の論理層 (または *層*) に分割されるデータ中心のアプリケーションです。 言い換えれば、n 層データ アプリケーションは、複数のプロジェクトに分離されたアプリケーションであり、データ アクセス層、ビジネス ロジック層、およびプレゼンテーション層がそれぞれ独自のプロジェクトに含まれています。 詳細については、「 [N 層データアプリケーションの概要](../data-tools/n-tier-data-applications-overview.md)」を参照してください。

TableAdapter およびデータセット クラスを別々のプロジェクトに生成できるように、型指定されたデータセットが強化されました。 これにより、アプリケーション層を分離して、n 層データ アプリケーションをすばやく生成できます。

型指定されたデータセットで n 層をサポートすることで、アプリケーションアーキテクチャを n 層設計に反復的に開発できます。また、コードを複数のプロジェクトに手動で分離する必要もなくなります。 **データセットデザイナー** を使用したデータレイヤーのデザインを開始します。 アプリケーション アーキテクチャを n 層デザインにする準備ができたら、データセット クラスが別個のプロジェクトに生成されるようにデータセットの **[DataSet プロジェクト]** プロパティを設定します。

## <a name="reference"></a>関連項目

- <xref:System.Data.DataSet>
- <xref:System.Data.TypedTableBase%601>

## <a name="see-also"></a>関連項目

- [N 層データアプリケーションの概要](../data-tools/n-tier-data-applications-overview.md)
- [チュートリアル: n 層データアプリケーションの作成](../data-tools/walkthrough-creating-an-n-tier-data-application.md)
- [n 層アプリケーションの TableAdapters にコードを追加する](../data-tools/add-code-to-tableadapters-in-n-tier-applications.md)
- [n 層アプリケーションのデータセットにコードを追加する](../data-tools/add-code-to-datasets-in-n-tier-applications.md)
- [n 層データセットに検証を追加する](../data-tools/add-validation-to-an-n-tier-dataset.md)
- [データセットと TableAdapters を別々のプロジェクトに分離する](../data-tools/separate-datasets-and-tableadapters-into-different-projects.md)
- [階層更新](../data-tools/hierarchical-update.md)
- [Visual Studio のデータセット ツール](../data-tools/dataset-tools-in-visual-studio.md)
- [Visual Studio でのデータへのアクセス](../data-tools/accessing-data-in-visual-studio.md)
- [Tableadapter の作成および構成](../data-tools/create-and-configure-tableadapters.md)
- [LINQ to SQL を使用した N 層とリモートアプリケーション](/dotnet/framework/data/adonet/sql/linq/n-tier-and-remote-applications-with-linq-to-sql)
