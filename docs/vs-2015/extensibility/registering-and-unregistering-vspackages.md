---
title: Vspackage | の登録と登録解除Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- registration, VSPackages
- VSPackages, registering
ms.assetid: e25e7a46-6a55-4726-8def-ca316f553d6b
caps.latest.revision: 36
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1f6bc85fb00c15831dcf1a9f64e4b886272df218
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68193816"
---
# <a name="registering-and-unregistering-vspackages"></a>VSPackage の登録と登録解除
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

属性を使用して VSPackage を登録しますが、  
  
## <a name="registering-a-vspackage"></a>VSPackage の登録  
 属性を使用して、マネージ Vspackage の登録を制御できます。 すべての登録情報は、pkgdef ファイルに含まれています。 ファイルベースの登録の詳細については、「 [Createpkgdef ユーティリティ](../extensibility/internals/createpkgdef-utility.md)」を参照してください。  
  
 次のコードは、標準の登録属性を使用して VSPackage を登録する方法を示しています。  
  
```csharp  
[PackageRegistration(UseManagedResourcesOnly = true)]  
[Guid("0B81D86C-0A85-4f30-9B26-DD2616447F95")]  
public sealed class BasicPackage : Package  
{. . .}  
```  
  
## <a name="unregistering-an-extension"></a>拡張機能の登録解除  
 さまざまな Vspackage を実験していて、実験用インスタンスから削除する必要がある場合は、 **Reset** コマンドを実行するだけで済みます。 コンピューターのスタートページで **Visual Studio の実験用インスタンスをリセット** するか、コマンドラインから次のコマンドを実行します。  
  
```vb  
<location of Visual Studio 2015 install>\"Microsoft Visual Studio 14.0\VSSDK\VisualStudioIntegration\Tools\Bin\CreateExpInstance.exe" /Reset /VSInstance=14.0 /RootSuffix=Exp  
```  
  
 Visual Studio の開発インスタンスにインストールした拡張機能をアンインストールする場合は、[ツール]、[ **拡張機能と更新プログラム**] の順に選択し、拡張機能を見つけて、[ **アンインストール**] をクリックします。  
  
 何らかの理由で、拡張機能のアンインストールでこれらのメソッドのいずれも成功しない場合は、次のようにコマンドラインから VSPackage アセンブリの登録を解除できます。  
  
```  
<location of Visual Studio 2015 install>\"Microsoft Visual Studio 14.0\VSSDK\VisualStudioIntegration\Tools\Bin\regpkg” /unregister <pathToVSPackage assembly>  
```  
  
## <a name="see-also"></a>参照  
 [VSPackages](../extensibility/internals/vspackages.md)
