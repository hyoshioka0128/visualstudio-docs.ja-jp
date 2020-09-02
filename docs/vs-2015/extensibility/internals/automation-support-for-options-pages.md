---
title: オプションページのオートメーションサポート |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Tools Options pages [Visual Studio SDK], automation support
- automation [Visual Studio SDK], creating Tools Options pages
ms.assetid: 0b25b82c-7432-4e0a-9e84-350269ba8260
caps.latest.revision: 30
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7cb2634f5a16c62222cf360065cae0c22aef6667
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68157245"
---
# <a name="automation-support-for-options-pages"></a>オプション ページのオートメーションのサポート
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Vspackage では、の [**ツール**] メニュー ([ツール] [オプション] ページ) にカスタム**オプション**のダイアログボックスを表示し、オートメーションモデルで使用できるようにすることができ [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。  
  
## <a name="tools-options-pages"></a>ツールオプションページ  
 **ツールオプション**ページを作成するには、VSPackage が、VSPackage によって実装されたメソッドの実装 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A> (または、メソッドのマネージコード) を通じて環境に返されるユーザーコントロールの実装を提供する必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A> ます。  
  
 これは省略可能ですが、オートメーションモデルを通じてこの新しいページにアクセスできるようにすることを強くお勧めします。 これを行うには、次の手順を実行します。  
  
1. <xref:EnvDTE._DTE.Properties%2A>IDispatch によって派生したオブジェクトの実装を通じて、オブジェクトを拡張します。  
  
2. メソッドの実装 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> (または、メソッドのマネージコード <xref:Microsoft.VisualStudio.Shell.Package.GetAutomationObject%2A> ) を IDispatch で派生したオブジェクトに返します。  
  
3. オートメーションコンシューマーが <xref:EnvDTE._DTE.Properties%2A> カスタム **オプション** プロパティページでメソッドを呼び出すと、環境はメソッドを使用して、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> カスタム **ツールオプション** ページのオートメーション実装を取得します。  
  
4. 次に、VSPackage のオートメーションオブジェクトを使用して、 <xref:EnvDTE.Property> によって返される各を指定し <xref:EnvDTE._DTE.Properties%2A> ます。  
  
   カスタムツールオプションページを実装するサンプルについては、「 [Vssdk のサンプル](../../misc/vssdk-samples.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [プロジェクト オブジェクトの公開](../../extensibility/internals/exposing-project-objects.md)
