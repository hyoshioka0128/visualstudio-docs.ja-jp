---
title: カスタムエディターでのドキュメントデータとドキュメントビュー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - document data and document view
ms.assetid: 71eea623-f566-4feb-84cd-ca1ba71bc493
caps.latest.revision: 24
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2f73ffde43f2ef3608ae492a9643f7920243d818
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204687"
---
# <a name="document-data-and-document-view-in-custom-editors"></a>カスタム エディターでのドキュメント データとドキュメント ビュー
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

カスタムエディターは、ドキュメントデータオブジェクトとドキュメントビューオブジェクトの2つの部分で構成されます。 名前が示すように、ドキュメントデータオブジェクトは表示されるテキストデータを表し、ドキュメントビューオブジェクト (または "ビュー") は、ドキュメントデータオブジェクトを表示する1つ以上のウィンドウを表します。  
  
## <a name="document-data-object"></a>ドキュメントデータオブジェクト  
 ドキュメントデータオブジェクトは、テキストバッファー内のテキストのデータ表現です。 これは、ドキュメントのテキストやその他の情報を格納し、ドキュメントの永続化を処理し、データの複数のビューを有効にする COM オブジェクトです。 詳細については、「  
  
 <xref:EnvDTE80.Window2.DocumentData%2A> および [ドキュメントウィンドウ](../extensibility/internals/document-windows.md)。  
  
 カスタムエディターとデザイナーでは、 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> オブジェクトまたは独自のカスタムバッファーを使用することを選択できます。 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> 標準エディターの簡略化された埋め込みモデルに従い、複数のビューをサポートし、複数のビューを管理するために使用されるイベントインターフェイスを提供します。  
  
## <a name="document-view-object"></a>ドキュメントビューオブジェクト  
 コードやその他のテキストを表示するウィンドウは、ドキュメントビューまたはビューと呼ばれます。 エディターを作成するときに、1つのビューを選択することができます。1つのウィンドウにテキストが表示されます。複数のビューでは、複数のウィンドウにテキストが表示されます。 選択は、アプリケーションによって異なります。 たとえば、サイドバイサイド編集が必要な場合は、複数のビューを選択します。 各ビューは、ドキュメントテーブル (RDT) を実行している統合開発環境の (IDE) のエントリに関連付けられています。 ビューウィンドウは、プロジェクトまたはオブジェクトに属して <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> います。  
  
 エディターでドキュメントデータオブジェクトの複数のビューがサポートされている場合は、ドキュメントデータオブジェクトとドキュメントビューオブジェクトが別々である必要があります。 それ以外の場合は、グループ化することができます。 詳細については、「 [複数のドキュメントビューのサポート](../extensibility/supporting-multiple-document-views.md)」を参照してください。  
  
 IDE は、実行中のドキュメントテーブル内の各エントリの項目識別子 (ItemID) を照合することによって、イベント (たとえば、ドキュメントを含むソリューションが閉じられたとき) をビューに通知します。 詳細については、「 [Document Table の実行](../extensibility/internals/running-document-table.md)」を参照してください。  
  
 カスタムエディターのビューを作成するには、2つのオプションがあります。 1つは、埋め込み先アクティブ化モデルです。このモデルでは、ActiveX コントロールまたはドキュメントデータオブジェクトを使用して、ビューがウィンドウでホストされます。 2つ目は簡略化された埋め込みモデルで、ビューはでホストされ、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane> ウィンドウコマンドを処理するために実装されます。 インプレースアクティブ化モデルの詳細については、「 [インプレースアクティブ化](../misc/in-place-activation.md)」を参照してください。 簡略化された埋め込みモデルについては、「簡略化された [埋め込み](../extensibility/simplified-embedding.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [複数のドキュメントビューのサポート](../extensibility/supporting-multiple-document-views.md)   
 [簡略化された埋め込み](../extensibility/simplified-embedding.md)   
 [方法: ドキュメントデータにビューをアタッチする](../extensibility/how-to-attach-views-to-document-data.md)   
 [ドキュメントロック所有者の管理](../extensibility/document-lock-holder-management.md)   
 [単一および複数のタブのビュー](../extensibility/single-and-multi-tab-views.md)   
 [標準ドキュメントの保存](../extensibility/internals/saving-a-standard-document.md)   
 [永続化と実行中のドキュメントテーブル](../extensibility/internals/persistence-and-the-running-document-table.md)   
 [プロジェクト内のファイルを開くエディターの決定](../extensibility/internals/determining-which-editor-opens-a-file-in-a-project.md)   
 [エディター ファクトリ](../extensibility/editor-factories.md)
