---
title: '方法: Windows の自動化を提供する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK], tool windows
- tool windows, automation
ms.assetid: 512ab2a4-7987-4912-8f40-8804bf66f829
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7ea7b79df4e7f3748ec2bc7f5e57c6ecb7dfca5b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68191849"
---
# <a name="how-to-provide-automation-for-windows"></a>方法: Windows 向けのオートメーションの提供
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

ドキュメントとツールウィンドウの自動化を提供できます。 オートメーションオブジェクトをウィンドウで使用できるようにする場合は常にオートメーションを提供することをお勧めします。また、作業リストの場合と同様に、事前に作成されたオートメーションオブジェクトが環境に用意されていません。  
  
## <a name="automation-for-tool-windows"></a>ツールウィンドウの自動化  
 環境では、次の手順で説明するように標準のオブジェクトを返すことによって、ツールウィンドウの自動化を提供し <xref:EnvDTE.Window> ます。  
  
#### <a name="to-provide-automation-for-tool-windows"></a>ツールウィンドウの自動化を提供するには  
  
1. オブジェクトを <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> 取得するには、as パラメーターを指定して環境でメソッドを呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID> `VSFPROPID` `Window` ます。  
  
2. 呼び出し元がを通じて、ツールウィンドウの VSPackage 固有のオートメーションオブジェクトを要求すると、 <xref:EnvDTE.Window.Object%2A> 環境は `QueryInterface` `IExtensibleObject` 、、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject> またはインターフェイスを呼び出し `IDispatch` ます。 `IExtensibleObject`と `IVsExtensibleObject` の両方がメソッドを提供し <xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject.GetAutomationObject%2A> ます。  
  
3. その後、環境がメソッドを渡すときに `GetAutomationObject` `NULL` 、VSPackage 固有のオブジェクトを返すことによって応答します。  
  
4. `QueryInterface`との呼び出し `IExtensibleObject` が失敗した場合 `IVsExtensibleObject` 、環境は `QueryInterface` を呼び出し `IDispatch` ます。  
  
## <a name="automation-for-document-windows"></a>ドキュメントウィンドウの自動化  
 標準 <xref:EnvDTE.Document> オブジェクトは環境からも使用できますが、 `T:EnvDTE.Document` インターフェイスを実装してに応答することによって、エディターはオブジェクトの独自の実装を持つことができ `IExtensibleObject` `GetAutomationObject` ます。  
  
 また、エディターは、 <xref:EnvDTE.Document.Object%2A> インターフェイスまたはインターフェイスを実装することによって、メソッドを通じて取得される VSPackage 固有のオートメーションオブジェクトを提供でき `IVsExtensibleObject` `IExtensibleObject` ます。 [Vssdk サンプル](../../misc/vssdk-samples.md)は、RTF ドキュメント固有のオートメーションオブジェクトを提供します。  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject>
