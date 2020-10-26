---
title: ファイル名拡張子に対する動詞の登録 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- verbs, registering
ms.assetid: 81a58e40-7cd0-4ef4-a475-c4e1e84d6e06
caps.latest.revision: 17
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: dbd97310163a4eb3ae5502c6341dc73322ca653d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65685268"
---
# <a name="registering-verbs-for-file-name-extensions"></a>ファイル名拡張子の動詞を登録する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通常、ファイル名拡張子とアプリケーションの関連付けには、ユーザーがファイルをダブルクリックしたときに発生する優先的な操作があります。 この優先アクションは、アクションに対応する動詞 (たとえば、open) にリンクされています。  
  
 HKEY_CLASSES_ROOT \\ *progid*\ shellにあるシェルキーを使用して、拡張機能のプログラム識別子 (progid) に関連付けられている動詞を登録できます。 詳細については、「 [ファイルの種類](https://msdn.microsoft.com/library/windows/desktop/cc144148\(v=vs.85\).aspx)」を参照してください。  
  
## <a name="registering-standard-verbs"></a>登録 (標準動詞を)  
 オペレーティングシステムは、次の標準動詞を認識します。  
  
- [ファイル]  
  
- [編集]  
  
- [再生]  
  
- 印刷  
  
- プレビュー  
  
  可能な限り、標準動詞を登録します。 最も一般的な選択は、Open 動詞です。 ファイルを開いてファイルを編集するときに明確な違いがある場合にのみ、Edit 動詞を使用します。 たとえば、.htm ファイルを開くと、ブラウザーに表示されます。一方、.htm ファイルを編集すると、HTML エディターが起動します。 標準動詞は、オペレーティングシステムのロケールでローカライズされます。  
  
> [!NOTE]
> 標準動詞を登録するときは、Open キーの既定値を設定しないでください。 既定値には、メニューの表示文字列が含まれています。 オペレーティングシステムは、標準の動詞にこの文字列を提供します。  
  
 ユーザーがファイルを開いたときにの新しいインスタンスを開始するには、プロジェクトファイルを登録する必要があり [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ます。 次の例は、プロジェクトの標準的な動詞登録を示してい [!INCLUDE[csprcs](../includes/csprcs-md.md)] ます。  
  
```  
[HKEY_CLASSES_ROOT\.csproj]  
@="VisualStudio.csproj.8.0"  
  
[HKEY_CLASSES_ROOT\.csproj\OpenWithList]  
[HKEY_CLASSES_ROOT\.csproj\OpenWithList\VSLauncher.exe]  
@=""  
  
[HKEY_CLASSES_ROOT\.csproj\OpenWithProgids]  
"VisualStudio.csproj.8.0"=""  
  
[HKEY_CLASSES_ROOT\Applications\VSLauncher.exe]  
[HKEY_CLASSES_ROOT\Applications\VSLauncher.exe\Shell]  
[HKEY_CLASSES_ROOT\Applications\VSLauncher.exe\Shell\Open]  
[HKEY_CLASSES_ROOT\Applications\VSLauncher.exe\Shell\Open\Command]  
@="C:\\Program Files\\Common Files\\Microsoft Shared\\MSEnv\\VSLauncher.exe \"%1\""  
  
[HKEY_CLASSES_ROOT\VisualStudio.csproj.8.0]  
@="C# Project file"  
  
[HKEY_CLASSES_ROOT\VisualStudio.csproj.8.0\DefaultIcon]  
@="C:\\VisualStudioPath\\VC#\\VCSPackages\\csproj.dll,0"  
  
[HKEY_CLASSES_ROOT\VisualStudio.csproj.8.0\shell]  
[HKEY_CLASSES_ROOT\VisualStudio.csproj.8.0\shell\Open]  
[HKEY_CLASSES_ROOT\VisualStudio.csproj.8.0\shell\Open\Command]  
@="\"C:\\Program Files\\Common Files\\Microsoft Shared\\MSEnv\\VSLauncher.exe\" \"%1\""  
```  
  
 の既存のインスタンスでファイルを開くには [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 、DDEEXEC キーを登録します。 次の例は、.cs ファイルの標準的な動詞登録を示してい [!INCLUDE[csprcs](../includes/csprcs-md.md)] ます。  
  
```  
[HKEY_CLASSES_ROOT\.cs]  
@="VisualStudio.cs.8.0"  
  
[HKEY_CLASSES_ROOT\.cs\OpenWithList]  
[HKEY_CLASSES_ROOT\.cs\OpenWithList\devenv.exe]  
@=""  
  
[HKEY_CLASSES_ROOT\.cs\OpenWithProgids]  
"VisualStudio.cs.8.0"=""  
  
[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0]  
@="C# Source file"  
  
[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\DefaultIcon]  
@="C:\\VisualStudioPath\\VC#\\VCSPackages\\csproj.dll,1"  
  
[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell]  
[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell\Open]  
[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell\Open\Command]  
@="\"C:\\VisualStudioPath\\Common7\\IDE\\devenv.exe\" /dde \"%1\""  
  
[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell\Open\ddeexec]  
@="Open(\"%1\")"  
  
[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell\Open\ddeexec\Application]  
@="VisualStudio.8.0"  
  
[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell\Open\ddeexec\Topic]  
@="system"  
```  
  
## <a name="setting-the-default-verb"></a>既定の動詞の設定  
 既定の動詞は、ユーザーがエクスプローラーでファイルをダブルクリックしたときに実行されるアクションです。 既定の動詞は、HKEY_CLASSES_ROOT \\ *progid*\ シェルキーの既定値として指定された動詞です。 値が指定されていない場合、既定の動詞は HKEY_CLASSES_ROOT \\ *progid*\ シェルキーリストで指定されている最初の動詞です。  
  
> [!NOTE]
> サイドバイサイド展開で拡張機能の既定の動詞を変更する場合は、インストールと削除に与える影響について検討してください。 インストール中に、元の既定値が上書きされます。  
  
## <a name="see-also"></a>参照  
 [side-by-side のファイルの関連付けを管理する](../extensibility/managing-side-by-side-file-associations.md)
