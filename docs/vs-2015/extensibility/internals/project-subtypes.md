---
title: プロジェクトのサブタイプ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], subtypes
- project subtypes [Visual Studio SDK]
ms.assetid: d235b47b-cf11-4d47-a63f-e33d9d16105d
caps.latest.revision: 21
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5ad1e105d43c40782b13d8799b20626e57363c2f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841389"
---
# <a name="project-subtypes"></a>プロジェクト サブタイプ
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

プロジェクトのサブタイプを使用すると、のプロジェクトシステムの動作をカスタマイズまたはフレーバーでき [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。 カスタマイズには、プロジェクトファイルへの追加データの保存、[ **新しい項目の追加** ] ダイアログボックスでの項目の追加またはフィルター処理、アセンブリのデバッグと配置の方法の制御、および [プロジェクト **プロパティページ** ] ダイアログボックスの拡張が含まれます。 Vspackage は、COM 集計を使用してプロジェクトのサブタイプを実装します。  
  
> [!NOTE]
> Visual C++ プロジェクトシステムでは、プロジェクトのサブタイプはサポートされていません。 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] では、プロジェクトのサブタイプを使用して、SQL Server およびスマートデバイスプロジェクトを実装します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [プロジェクト サブタイプのデザイン](../../extensibility/internals/project-subtypes-design.md)  
 プロジェクトのサブタイプの概念について説明します。  
  
 [プロジェクト サブタイプの初期化シーケンス](../../extensibility/internals/initialization-sequence-of-project-subtypes.md)  
 環境別のプログラムによるプロジェクトのサブタイプ初期化シーケンスについて説明し [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。  
  
 [プロジェクト サブタイプによって拡張されるプロパティとメソッド](../../extensibility/internals/properties-and-methods-extended-by-project-subtypes.md)  
 プロジェクトのサブタイプを使用して最も頻繁に拡張される機能とメソッドについて詳しく説明します。  
  
 [MSBuild プロジェクト ファイルでのデータの保持](../../extensibility/internals/persisting-data-in-the-msbuild-project-file.md)  
 プロジェクトファイルにデータを保存する方法と、を使用してプロジェクトファイルのデータをプロジェクトのサブタイプ集計レベルで保持する方法について説明し <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> ます。  
  
 [プロジェクト プロパティのユーザー インターフェイス](../../extensibility/internals/project-property-user-interface.md)  
 プロジェクトのサブタイプでプロジェクトの [ **プロパティページ** ] ダイアログボックスを変更する方法について説明します。  
  
 [ベース プロジェクトのオブジェクト モデルの拡張](../../extensibility/internals/extending-the-object-model-of-the-base-project.md)  
 プロジェクトのサブタイプがオートメーションエクステンダーを使用してオートメーションオブジェクトモデルを拡張する方法について説明します。  
  
 [[新しい項目の追加] ダイアログ ボックスへの投稿](../../extensibility/internals/contributing-to-the-add-new-item-dialog-box.md)  
 [ **新しい項目の追加** ] ダイアログボックスに項目を追加する方法について説明します。  
  
 [プロジェクト ファイルでのデータの保存](../../extensibility/saving-data-in-project-files.md)  
 マネージパッケージフレームワーク (MPF) を使用して、プロジェクトのサブタイプがプロジェクトファイル内のサブタイプ固有のデータを保存および取得する方法について説明します。  
  
 [特別な展開の処理](../../extensibility/internals/handling-specialized-deployment.md)  
 プロジェクトのサブタイプがインターフェイスを実装することによって特殊な配置動作を提供する方法について説明 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg> します。  
  
 [プロパティ ページの追加と削除](../../extensibility/adding-and-removing-property-pages.md)  
 プロジェクトデザイナーでのプロパティページの追加と削除について説明します。  
  
## <a name="related-sections"></a>関連項目  
 [プロジェクトの種類](../../extensibility/internals/project-types.md)  
 プロジェクトの詳細に関するトピックへのリンクを示し [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。
