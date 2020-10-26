---
title: で使用される代替文字列。Pkgdef と。Pkgundef ファイル |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio shell, isolated mode%2C .pkgdef and .pkgundef files
ms.assetid: b1755d63-d794-4fd7-864b-70a9684881c2
caps.latest.revision: 5
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 47434d9d1dfcedeeaea330b1d65645d7a632c6e6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68160541"
---
# <a name="substitution-strings-used-in-pkgdef-and-pkgundef-files"></a>.pkgdef および .pkgundef ファイルで使用されている代替文字列
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

次に示す置換文字列は、Visual Studio 分離シェルアプリケーション用に定義した、pkgdef ファイルと pkgdef ファイルで使用できます。  
  
## <a name="substitution-strings"></a>置換文字列  
  
|String|説明|  
|------------|-----------------|  
|$=*RegistryEntry*$|*Registryentry*エントリの値。 レジストリエントリの文字列が円記号 () で終わっている場合は、 \\ レジストリサブキーの既定値が使用されます。 たとえば、置換文字列 $ = HKEY_CURRENT_USER \ 環境 \Temp $ は、現在のユーザーの一時フォルダーに展開されます。|  
|$AppName $|AppEnv.dll エントリポイントに渡されるアプリケーションの限定名。 修飾名は、アプリケーション名、アンダースコア、およびアプリケーションオートメーションオブジェクトのクラス識別子 (CLSID) で構成されます。これは、プロジェクトの pkgdef ファイルのこの Versiondteclsid 設定の値としても記録されます。|  
|$AppDataLocalFolder|このアプリケーションの% LOCALAPPDATA% の下にサブフォルダーがあります。|  
|$BaseInstallDir $|Visual Studio がインストールされている場所の完全パス。|  
|$CommonFiles $|% CommonProgramFiles% 環境変数の値。|  
|$MyDocuments $|現在のユーザーの [マイドキュメント] フォルダーの完全パス。|  
|$PackageFolder $|アプリケーションのパッケージアセンブリファイルが格納されているディレクトリの完全パス。|  
|$ProgramFiles $|% ProgramFiles% 環境変数の値。|  
|$RootFolder $|アプリケーションのルートディレクトリの完全パス。|  
|$RootKey $|アプリケーションのルートレジストリキー。 既定では、ルートは HKEY_CURRENT_USER \ software \\ *CompanyName* \\ *ProjectName* \\ *VersionNumber*にあります (アプリケーションが実行されている場合、_Config がこのキーに追加されます)。 これは、 *SolutionName*ファイルの registryroot 値によって設定されます。<br /><br /> $RootKey $ 文字列を使用して、アプリケーションのサブキーの下にあるレジストリ値を取得できます。 たとえば、文字列 "$ = $RootKey $ \AppIcon $" は、アプリケーションのルートサブキーの下にある AppIcon エントリの値を返します。<br /><br /> パーサーは、pkgdef ファイルを順番に処理し、エントリが既に定義されている場合にのみ、アプリケーションサブキーの下にあるレジストリエントリにアクセスできます。|  
|$ShellFolder $|Visual Studio がインストールされている場所の完全パス。|  
|$System $|Windows\system32 フォルダーです。|  
|$WINDIR $|Windows フォルダー。|  
  
 パーサーが置換文字列を認識しない場合、またはレジストリエントリまたは環境変数の値を判断できない場合は、文字列のその部分に対する置換は実行されません。
