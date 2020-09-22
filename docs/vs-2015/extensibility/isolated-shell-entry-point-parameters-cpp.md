---
title: 分離シェルエントリポイントパラメーター (C++) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Shell [Visual Studio], isolated mode%2C Start entry point
- Visual Studio shell, isolated mode%2C Start entry point
ms.assetid: 18f4b18b-2173-4afa-ba0a-42fe33e61118
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 9e736343212c4bf6acd833f5740b996c6c032c3f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842140"
---
# <a name="isolated-shell-entry-point-parameters-c"></a>分離シェル エントリ ポイントのパラメーター (C++)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio シェルベースのアプリケーションが起動すると、Visual Studio シェルの開始エントリポイントが呼び出されます。 次の設定は、シェルの開始エントリポイントへの呼び出しでオーバーライドできます。 各設定の説明については、「」を参照してください [。Pkgdef ファイル](../extensibility/modifying-the-isolated-shell-by-using-the-dot-pkgdef-file.md)。  
  
- 許可された追加  
  
- AllowsDroppedFilesOnMainWindow  
  
- AppName  
  
- CommandLineLogo  
  
- DefaultHomePage  
  
- Defaultプロジェクトの場所  
  
- DefaultSearchPage  
  
- DefaultUserFilesFolderRoot  
  
- DisableOutputWindow  
  
- HideMiscellaneousFilesByDefault  
  
- HideSolutionConcept  
  
- Newprojdlgexistingtemplates Hdr  
  
- Newprojdlgslntreのタイトル  
  
- SolutionFileCreatorIdentifier  
  
- SolutionFileExt  
  
- UserFilesSubFolderName  
  
- UserOptsFileExt  
  
  Visual Studio Shell 分離テンプレートによってソースファイル *solutionName*が作成されます。 *solutionName* は、アプリケーションのソリューション名です。 このファイルは、アプリケーションのメインエントリポイントである _tWinMain 関数を定義します。 この関数は、シェルの開始エントリポイントを呼び出します。  
  
  アプリケーションの起動時にこれらの設定を変更することによって、アプリケーションの動作を変更できます。  
  
## <a name="parameters"></a>パラメーター  
 Visual Studio シェルの開始エントリポイントは、5つのパラメーターを定義します。 最初の4つのパラメーターは変更しないでください。 5番目のパラメーターは、設定のオーバーライドリストを受け取ります。 シェルの開始エントリポイントは、アプリケーションのメインエントリポイントから呼び出されます。  
  
 シェルの開始エントリポイントには、次のシグネチャがあります。  
  
```  
typedef int (__cdecl *STARTFCN)(LPSTR, LPWSTR, int, GUID *, WCHAR *pszSettings);  
```  
  
 アプリケーション設定を上書きしない場合は、設定のオーバーライドパラメーターの値を null ポインターとしてそのままにします。  
  
 1つまたは複数の設定をオーバーライドするには、オーバーライドする設定を含む Unicode 文字列を渡します。 文字列は、名前と値のペアのセミコロン区切りのリストです。 各ペアには、オーバーライドする設定の名前、等号 (=)、およびその後に設定に適用する値が含まれます。  
  
> [!NOTE]
> Unicode 文字列に空白を含めないでください。  
  
 ブール値の設定では、次の文字列は値 true を表します。他のすべての文字列は、値 false を表します。 これらの文字列は大文字と小文字が区別されません。  
  
- \+  
  
- 1  
  
- -1  
  
- on  
  
- true  
  
- はい  
  
## <a name="example"></a>例  
 アドインを無効にして、アプリケーションの既定のプロジェクトの場所を変更するには、最後のパラメーターを "Addins Allowed = false; Defaultprojects Location =%USERPROFILE%\temp" に設定します。  
  
## <a name="see-also"></a>参照  
 [分離シェルのカスタマイズ](../extensibility/customizing-the-isolated-shell.md)   
 [.pkgdef ファイル](../extensibility/modifying-the-isolated-shell-by-using-the-dot-pkgdef-file.md)
