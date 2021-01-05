---
title: ファイル名拡張子に対する動詞の登録 |Microsoft Docs
description: シェルキーを使用して、ファイル名拡張子のプログラム識別子に関連付けられている動詞を登録する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- verbs, registering
ms.assetid: 81a58e40-7cd0-4ef4-a475-c4e1e84d6e06
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: df0dfe90bd5e3bccbb6bb0f9dab400082f539fbf
ms.sourcegitcommit: dd96a95d87a039525aac86abe689c30e2073ae87
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/04/2021
ms.locfileid: "97863042"
---
# <a name="register-verbs-for-file-name-extensions"></a>ファイル名拡張子の動詞を登録する
通常、ファイル名拡張子とアプリケーションの関連付けには、ユーザーがファイルをダブルクリックしたときに発生する優先的な操作があります。 この優先アクションは、アクションに対応する動詞 (たとえば、open) にリンクされています。

 拡張機能のプログラム識別子 (ProgID) に関連付けられている動詞は、 **HKEY_CLASSES_ROOT \{ progid} \ シェル** にあるシェルキーを使用して登録できます。 詳細については、「 [ファイルの種類](/windows/desktop/shell/fa-file-types)」を参照してください。

## <a name="register-standard-verbs"></a>標準動詞の登録
 オペレーティングシステムは、次の標準動詞を認識します。

- [ファイル]

- 編集

- Play

- 印刷

- プレビュー

  可能な限り、標準動詞を登録します。 最も一般的な選択は、Open 動詞です。 ファイルを開いてファイルを編集するときに明確な違いがある場合にのみ、Edit 動詞を使用します。 たとえば、 *.htm* ファイルを開くと、ブラウザーに表示されます。一方、 *.htm* ファイルを編集すると、HTML エディターが起動します。 標準動詞は、オペレーティングシステムのロケールでローカライズされます。

> [!NOTE]
> 標準動詞を登録するときは、Open キーの既定値を設定しないでください。 既定値には、メニューの表示文字列が含まれています。 オペレーティングシステムは、標準の動詞にこの文字列を提供します。

 ユーザーがファイルを開いたときにの新しいインスタンスを開始するには、プロジェクトファイルを登録する必要があり [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ます。 次の例は、プロジェクトの標準的な動詞登録を示してい [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] ます。

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

 の既存のインスタンスでファイルを開くには [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 、DDEEXEC キーを登録します。 次の例は、.cs ファイルの標準的な動詞登録を示してい [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] ます。

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

## <a name="set-the-default-verb"></a>既定の動詞を設定する
 既定の動詞は、ユーザーがエクスプローラーでファイルをダブルクリックしたときに実行されるアクションです。 既定の動詞は、 **HKEY_CLASSES_ROOT \\ *progid*\ シェル** キーの既定値として指定された動詞です。 値が指定されていない場合、既定の動詞は **HKEY_CLASSES_ROOT \\ *progid*\ シェル** キーリストで指定されている最初の動詞です。

> [!NOTE]
> サイドバイサイド展開で拡張機能の既定の動詞を変更する場合は、インストールと削除に与える影響について検討してください。 インストール中に、元の既定値が上書きされます。

## <a name="see-also"></a>関連項目
- [Side-by-side ファイルの関連付けの管理](../extensibility/managing-side-by-side-file-associations.md)
