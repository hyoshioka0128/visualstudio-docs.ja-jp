---
title: 分離シェル | の要素Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio shell, isolated mode
ms.assetid: f8d68c3d-9134-4a8f-b566-485956cd321e
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3a95b7da718f050357f6ecd79c90c389dd6085d5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204611"
---
# <a name="elements-of-the-isolated-shell"></a>分離シェルの要素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

分離シェルアプリケーションのレジストリ設定、実行時の設定、アプリケーションのエントリポイント、およびその vsct、pkgdef、および pkgdef ファイルを変更できます。  
  
## <a name="registry-settings"></a>レジストリの設定  
 Pkgdef と pkgdef の両方のファイルによって、分離シェルアプリケーションのレジストリ設定が変更されます。 アプリケーションを実行すると、レジストリ設定は次の順序で定義されます。  
  
 アプリケーションを実行すると、レジストリ設定は次の順序で定義されます。  
  
1. アプリケーションのレジストリキーが作成されます。  
  
2. レジストリは、指定されたキーとエントリを定義することによって、アプリケーションの pkgdef ファイルから更新されます。  
  
3. アプリケーションの一部であるすべてのパッケージについて、そのパッケージの pkgdef ファイルからレジストリが更新されます。 各パッケージは、パッケージの $RootKey $ \ Packages \\ {*vsPackageGuid*} キーを使用して、アプリケーションの pkgdef ファイルで定義されます。  
  
4. レジストリは、 *Visual STUDIO SDK インストールパス*\Common7\IDE\ShellExtensions\Platform ディレクトリの AppEnvConfig Def と baseconfig. pkgdef から更新されます。 これらのファイルは、Visual Studio の一部であり、Visual Studio Shell (分離モード) 再頒布可能パッケージの一部でもあります。  
  
5. レジストリは、指定されたキーとエントリを削除することによって、アプリケーションの pkgundef ファイルから更新されます。  
  
## <a name="run-time-settings"></a>実行時の設定  
 ユーザーが分離シェルアプリケーションを起動すると、Visual Studio シェルの開始エントリポイントが呼び出されます。 アプリケーションの設定は、アプリケーションの起動時に次のように定義されます。  
  
1. Visual Studio シェルは、アプリケーションレジストリで特定のキーを確認します。 キーの設定が開始エントリポイントの呼び出しで指定されている場合、その値はレジストリの値よりも優先されます。  
  
2. レジストリもエントリポイントパラメーターも設定の値を指定していない場合は、設定の既定値が使用されます。  
  
   ユーザーがコマンドラインからアプリケーションを起動すると、すべてのコマンドラインスイッチが、Devenv と同じ方法で処理される Visual Studio シェルに渡されます。 Devenv スイッチの詳細については、「 [Devenv コマンドラインスイッチ](../ide/reference/devenv-command-line-switches.md) 」と「Devenv [コマンドラインスイッチ (VSPackage Development 用](../extensibility/devenv-command-line-switches-for-vspackage-development.md))」を参照してください。 パッケージによるコマンドラインスイッチの登録方法の詳細については、「 [コマンドラインスイッチの追加](../extensibility/adding-command-line-switches.md)」を参照してください。  
  
## <a name="the-start-entry-point"></a>開始エントリポイント  
 Appenvstub.dll ファイルには、分離シェルにアクセスするためのエントリポイントが含まれています。 アプリケーションが起動すると、Appenvstub.dll の開始エントリポイントが呼び出されます。  
  
 開始エントリポイントに渡される最後のパラメーターの値を変更することによって、アプリケーションの動作を変更できます。 詳細については、「 [分離シェルエントリポイントパラメーター (C++)](../extensibility/isolated-shell-entry-point-parameters-cpp.md)」を参照してください。  
  
## <a name="the-vsct-file"></a>、.Vsct ファイル  
 Vsct ファイルを使用すると、アプリケーションで使用できる標準の Visual Studio UI 要素を指定できます。 詳細については、「」を参照してください [。Vsct ファイル](../extensibility/modifying-the-isolated-shell-by-using-the-dot-vsct-file.md)。  
  
## <a name="the-pkgundef-file"></a>、.Pkgundef ファイル  
 Visual Studio が既にインストールされているコンピューターにアプリケーションをインストールすると、そのアプリケーションに対して Visual Studio レジストリエントリのコピーが作成されます。 既定では、アプリケーションはコンピューターに既にインストールされている Vspackage を使用します。 Pkgundef ファイルを使用すると、Visual Studio シェルまたは拡張機能の特定の要素をアプリケーションから削除するために、レジストリエントリを除外できます。 詳細については、「」を参照してください [。Pkgundef ファイル](../extensibility/modifying-the-isolated-shell-by-using-the-dot-pkgundef-file.md)。  
  
 Pkgundef ファイルを使用すると、Visual Studio シェルまたは拡張機能の特定の要素をアプリケーションから削除するために、レジストリエントリを除外できます。 詳細については、「」を参照してください [。Pkgundef ファイル](../extensibility/modifying-the-isolated-shell-by-using-the-dot-pkgundef-file.md)。  
  
 除外できるパッケージ Guid のセットは、「 [Visual Studio の機能のパッケージ guid](../extensibility/package-guids-of-visual-studio-features.md)」に記載されています。  
  
## <a name="the-pkgdef-file"></a>、.Pkgdef ファイル  
 Pkgdef ファイルを使用すると、アプリケーションのインストール時に設定されるアプリケーションのレジストリエントリを定義できます。 Pkgdef ファイルの説明と、Visual Studio シェルで使用されるレジストリエントリの一覧については、「」を参照してください [。Pkgdef ファイル](../extensibility/modifying-the-isolated-shell-by-using-the-dot-pkgdef-file.md)。  
  
## <a name="substitution-strings"></a>置換文字列  
 Pkgdef および pkgdef ファイルで使用される代替文字列は、「」で使用されている代替文字列に記載されてい [ます。Pkgdef と。Pkgundef ファイル](../extensibility/substitution-strings-used-in-dot-pkgdef-and-dot-pkgundef-files.md)。  
  
## <a name="other-settings"></a>[その他の設定]  
 分離シェルアプリケーションが Microsoft.VisualStudio.GraphModel.dll に依存している場合は、分離シェルアプリケーションの .config ファイルに次のバインドリダイレクトを追加する必要があります。  
  
```  
<dependentAssembly>  
    <assemblyIdentity name="Microsoft.VisualStudio.GraphModel" publicKeyToken="b03f5f7f11d50a3a" culture="neutral" />  
    <bindingRedirect oldVersion="11.0.0.0" newVersion="12.0.0.0"/>  
</dependentAssembly>  
  
```
