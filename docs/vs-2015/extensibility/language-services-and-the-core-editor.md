---
title: 言語サービスとコアエディター |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - language services
ms.assetid: e03199a6-ad5f-4075-bfba-8d36865112b7
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1e708ffe796bfc9342bc20c3e7f20d5cf0d05058
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68180305"
---
# <a name="language-services-and-the-core-editor"></a>言語サービスとコア エディター
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio のエディターは、多くの場合、言語サービスに関連付けられています。 特に、言語サービスでは、構文の色分け、ステートメント入力候補、IntelliSense、およびテキストの書式設定が提供されます。  
  
## <a name="core-editors-and-document-data-objects"></a>コアエディターとドキュメントデータオブジェクト  
 コアエディターにアクセスするときは、ドキュメントデータおよびドキュメントビューオブジェクトを作成しません。 IDE では、これら2つのオブジェクトを作成および制御し、エディターファクトリの実装で適切な呼び出しを行うことによって、それらのオブジェクトへのハンドルを取得します。  
  
 詳細については、「 [プロジェクト内でファイルを開くエディターの決定](../extensibility/internals/determining-which-editor-opens-a-file-in-a-project.md)」を参照してください。  
  
## <a name="language-services-and-the-core-editor"></a>言語サービスとコア エディター  
 言語サービスを実装することにより、ドキュメントビューでのデータの表示方法を制御できます。 言語サービスは、特定の言語 (Visual C++ など) に固有の情報と動作を提供します。 テキストバッファーを作成し、開いているドキュメントのファイル名拡張子を決定すると、テキストバッファーによって、このファイル名拡張子に関連付けられている言語サービスがレジストリキーから特定されます (HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\Editors \\ {YOURLANGUAGESERVICE GUID})。 次に、標準の VSPackage 読み込みプロシージャによって VSPackage が読み込まれ、言語サービスのインスタンスが作成されます。  
  
 次の図は、基本的な言語サービスを示しています。  
  
 ![言語サービス モデル グラフィック](../extensibility/media/vslanguageservicemodel.gif "vsLanguageServiceModel")  
コアエディターと言語サービスオブジェクト  
  
 コアエディターのドキュメントデータオブジェクトはテキストバッファーと呼ばれ、オブジェクトによって表され <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> ます。 ドキュメントビューオブジェクトはテキストビューと呼ばれ、オブジェクトによって表され <xref:Microsoft.VisualStudio.TextManager.Interop.VsCodeWindow> ます。 この2つのオブジェクトは、言語サービスを通じて連携し、コアエディターの統合ビューを提供します。 テキストバッファーおよびテキストビューからの情報は、コードウィンドウと呼ばれるドキュメントウィンドウに表示されます。 コードウィンドウドキュメントは、コードウィンドウマネージャーによって管理されます。  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.VsCodeWindow>   
 [レガシ API を使用して言語サービスコンテキストを提供する](../extensibility/providing-a-language-service-context-by-using-the-legacy-api.md)   
 [IntelliSense のホスト](../extensibility/intellisense-hosting.md)   
 [含まれている言語](../extensibility/contained-languages.md)   
 [従来の言語サービスの開発](../extensibility/internals/developing-a-legacy-language-service.md)
