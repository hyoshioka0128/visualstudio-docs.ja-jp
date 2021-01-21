---
title: '方法: フィーチャーの依存関係を追加および削除するMicrosoft Docs'
description: Visual Studio のフィーチャーデザイナーを使用して、SharePoint ソリューションにフィーチャーの依存関係を追加および削除する方法を確認します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- MICROSOFT.VISUALSTUDIO.SHAREPOINT.DESIGNERS.CUSTOMDEPENDENCYWINDOW
- VS.SHAREPOINTTOOLS.RAD.FEATUREDESIGNERDEPENDENCY
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, features
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 5011db32123e77e9bf60c99459125302b2bf8264
ms.sourcegitcommit: 8e9c38da7bcfbe9a461c378083846714933a0e1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "96915363"
---
# <a name="how-to-add-and-remove-feature-dependencies"></a>方法: フィーチャーの依存関係を追加および削除する
  SharePoint 機能は、機能またはデータの他の機能に依存している場合があります。 このような場合は、機能の依存関係として、これらの他の機能をマークできます。 これにより、SharePoint サーバーは、機能がアクティブ化される前に依存機能がアクティブになるようにします。

## <a name="add-dependencies"></a>依存関係を追加する
 ソリューション内のその他の機能を依存関係として追加できます。 これにより、機能をインストールする前に、必要な機能がインストールされ、アクティブ化されるようにすることができます。

#### <a name="to-add-a-dependency-on-a-feature-in-the-solution"></a>ソリューションの機能に依存関係を追加するには

1. フィーチャーデザイナーを開き、[ **機能アクティブ化依存関係** ] ノードを展開し、[ **追加** ] ボタンをクリックします。

2. [ **フィーチャーアクティブ化依存関係の追加** ] ダイアログボックスで、[ **ソリューションの機能に依存関係を追加** する] オプションボタンを選択し、依存関係として追加する機能のタイトルを選択し、[ **追加** ] ボタンをクリックします。

     複数の機能を追加するには、Ctrl キーを **押し** ながら複数のタイトルを選択します。

## <a name="addi-custom-dependencies"></a>Addi カスタム依存関係
 SharePoint サーバーに既に配置されている機能を依存関係として追加できます。 これにより、SharePoint のアクティブ化プロセスによって、機能がインストールされる前にすべての依存機能がアクティブ化されているかどうかが確認されます。

#### <a name="to-add-a-dependency-by-the-feature-id"></a>機能 ID に依存関係を追加するには

1. フィーチャーデザイナーを開き、[ **機能アクティブ化依存関係** ] ノードを展開し、[ **追加** ] ボタンをクリックします。

2. [ **フィーチャーアクティブ化依存関係の追加** ] ダイアログボックスで、[ **カスタム依存関係を追加する** ] をクリックします。

3. [ **機能 ID** ] テキストボックスに、アクティブ化依存関係としてマークする機能の GUID を入力し、[ **追加** ] ボタンをクリックします。

## <a name="edit-custom-dependencies"></a>カスタム依存関係の編集
 前に追加したカスタム依存関係を編集できます。 ただし、ソリューション内の依存機能は削除のみ可能であり、編集することはできません。

#### <a name="to-change-a-dependency-on-a-feature-in-the-solution"></a>ソリューションの機能の依存関係を変更するには

1. フィーチャーデザイナーを開き、[ **機能アクティブ化依存関係** ] ノードを展開します。

2. 編集する機能の名前を選択し、[ **編集** ] ボタンをクリックします。

3. [ **カスタム機能アクティブ化依存関係の編集** ] ダイアログボックスで、タイトル、機能 ID、または説明を変更し、[ **送信** ] ボタンをクリックします。

## <a name="remove-dependencies"></a>依存関係の削除

#### <a name="to-remove-a-dependency-on-a-feature-in-the-solution"></a>ソリューション内のフィーチャーの依存関係を削除するには

1. フィーチャーデザイナーで、[ **機能アクティブ化依存関係** ] ノードを展開し、削除する機能の名前を選択して、[ **削除** ] ボタンをクリックします。

## <a name="see-also"></a>関連項目
- [SharePoint 機能の作成](../sharepoint/creating-sharepoint-features.md)
- [方法: SharePoint 機能をカスタマイズする](../sharepoint/how-to-customize-a-sharepoint-feature.md)
- [方法: SharePoint 機能に項目を追加および削除する](../sharepoint/how-to-add-and-remove-items-to-sharepoint-features.md)
