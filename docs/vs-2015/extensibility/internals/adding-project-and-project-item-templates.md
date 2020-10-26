---
title: プロジェクトおよびプロジェクト項目テンプレートの追加 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], adding
- project items [Visual Studio], adding
ms.assetid: 8c59217f-56e5-4540-a73b-cd10de189373
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4b68c9f4bbaed73603c46fc0beab77a308b8933d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68203861"
---
# <a name="adding-project-and-project-item-templates"></a>プロジェクト テンプレートとプロジェクト項目テンプレートの追加
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

独自のプロジェクトの種類を作成する場合は、標準の [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 統合開発環境 (IDE) のダイアログボックスを使用して、新しいプロジェクトとプロジェクト項目を追加するためのサポートを提供する必要があります。 次のトピックでは、プロジェクトおよびプロジェクト項目を追加するためのさまざまな手法について説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [プロジェクトのコンテキスト](../../extensibility/internals/project-context.md)  
 環境内の発生に関するコンテキスト情報の大部分がプロジェクトによって提供されることについて説明します。  
  
 [プロジェクトの優先順位](../../extensibility/internals/project-priority.md)  
 プロジェクト項目は通常、1つのプロジェクトのメンバーであるため、項目を開くために使用されるプロジェクトがあいまいになるのを防ぐことができます。  
  
 [その他のファイル プロジェクト](../../extensibility/internals/miscellaneous-files-project.md)  
 プロジェクト内のファイルを開くために使用できる2種類のエディターに関する情報と、プロジェクト項目を開いたときに使用するエディターを決定するためにプロジェクトが果たす役割について説明します。  
  
 [プロジェクトと項目テンプレートの登録](../../extensibility/internals/registering-project-and-item-templates.md)  
 プロジェクトが作成されたときの動作について説明 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] します。  
  
 [[新しい項目の追加] ダイアログ ボックスへの項目の追加](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)  
 [ **新しい項目の追加** ] ダイアログボックスに項目を追加するプロセスについて説明します。  
  
 [[新しいプロジェクト] ダイアログ ボックスへの新しいディレクトリの追加](../../extensibility/internals/adding-directories-to-the-new-project-dialog-box.md)  
 VSPackage によって使用可能になったカスタムテンプレートを含む新しいディレクトリを登録する例を示します。  
  
 [[新しい項目の追加] ダイアログ ボックスへの新しいディレクトリの追加](../../extensibility/internals/adding-directories-to-the-add-new-item-dialog-box.md)  
 [ **新しい項目の追加** ] ダイアログボックスに新しいディレクトリのセットを登録する例を示します。  
  
 [プロジェクト システムを拡張するための IDE 定義コマンド](../../extensibility/internals/ide-defined-commands-for-extending-project-systems.md)  
 プロジェクトシステムの拡張に使用されるさまざまな種類のコマンド項目を一覧表示します。  
  
 [プロジェクトの拡張に通常使用されるオブジェクトの CATID](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)  
 、、およびの各プロジェクトシステムを拡張するために使用されるオブジェクトの Catid の一覧を示し [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] [!INCLUDE[csprcs](../../includes/csprcs-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] ます。  
  
## <a name="related-sections"></a>関連項目  
 [方法: プロジェクト固有のエディターを開く](../../extensibility/how-to-open-project-specific-editors.md)  
 プロジェクトの特定のエディターに本質的にバインドされている項目を開く手順について説明します。  
  
 [方法: 標準のエディターを開く](../../extensibility/how-to-open-standard-editors.md)  
 標準エディターを開く手順について説明します。  
  
 [プロジェクト サブタイプ](../../extensibility/internals/project-subtypes.md)  
 プロジェクトのサブタイプの概念に関するトピックへのリンクを示します。 プロジェクトのサブタイプにより [!INCLUDE[csprcs](../../includes/csprcs-md.md)] 、既存のプロジェクトとプロジェクトが拡張さ [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] れます。  
  
 [プロジェクトの種類](../../extensibility/internals/project-types.md)  
 新しいプロジェクトの種類をデザインする方法に関する情報を提供するその他のトピックへのリンクを示します。
