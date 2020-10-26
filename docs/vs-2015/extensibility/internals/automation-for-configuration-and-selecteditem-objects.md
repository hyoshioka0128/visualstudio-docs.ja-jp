---
title: Configuration オブジェクトと SelectedItem オブジェクトのオートメーション |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK], SelectedItem object
- automation [Visual Studio SDK], builds
ms.assetid: 120377f1-51aa-4445-b2f7-06ab7fc2b47f
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 42faf8127c1ab70d3470aa497a0cdab6058060f8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68157261"
---
# <a name="automation-for-configuration-and-selecteditem-objects"></a>構成および SelectedItem オブジェクトのためのオートメーション
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

では、ビルドと選択された項目プロセスを自動化でき [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。  
  
## <a name="automation-for-builds"></a>ビルドの自動化  
 ビルドまたは構成には、を実装するときに提供されるオートメーションモデルがあり <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider> ます。 詳しくは、「[ビルド構成について](../../ide/understanding-build-configurations.md)」をご覧ください。  
  
 VSPackage を作成し、構成オプションを制御する場合は、オートメーションモデルを使用する必要があります。  
  
## <a name="automation-for-selecteditem"></a>SelectedItem の Automation  
 `SelectedItem`Visual Studio には標準の実装が含まれているため、オブジェクトの実装を指定する必要はありません。 ただし、必要に応じてオブジェクトを実装することもでき `SelectedItem` ます。 VSITEMID をに設定して、インターフェイスを含むオブジェクトを実装 `SelectedItem` し、メソッドへの呼び出しに対する応答を返す必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A> <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID> ます。  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A>   
 [オートメーションモデルに貢献する](../../extensibility/internals/contributing-to-the-automation-model.md)   
 [ビルド構成について](../../ide/understanding-build-configurations.md)
