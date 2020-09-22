---
title: CreatePkgDef Utility |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- package definition
- create pkgdef
- pkgdef
- createpkgdef
ms.assetid: c745cb76-47a6-49ff-9eed-16af0f748e35
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 010ee75efd84f016b0eb68fa9f715102026a4678
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841408"
---
# <a name="createpkgdef-utility"></a>CreatePkgDef ユーティリティ
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

は、Visual Studio 拡張機能の .dll ファイルをパラメーターとして受け取り、.dll に付随する pkgdef ファイルを作成します。 Pkgdef ファイルには、拡張機能のインストール時にシステムレジストリに書き込まれるすべての情報が含まれています。  
  
> [!NOTE]
> Visual Studio SDK に含まれているほとんどのプロジェクトテンプレートは、ビルド処理の一部として、自動的に pkgdef ファイルを作成します。 このドキュメントは、手動でパッケージを作成する場合や、pkgdef の展開を使用するように既存のパッケージを変換する場合を対象としています。  
  
## <a name="syntax"></a>構文  
  
```  
CreatePkgDef /out=FileName [/codebase] [/assembly] AssemblyPath  
```  
  
## <a name="arguments"></a>引数  
 /out =`FileName`  
 必須です。 Pkgdef 出力ファイルの名前をに設定します `FileName` 。  
  
 /codebase  
 省略可能。 CodeBase ユーティリティに強制的に登録します。  
  
 /assembly  
 アセンブリユーティリティに登録を強制します。  
  
 `AssemblyPath`  
 Pkgdef を生成する元となる .dll ファイルのパス。  
  
## <a name="remarks"></a>注釈  
 Pkgdef ファイルを使用した拡張機能の展開では、以前のバージョンの Visual Studio のレジストリ要件が置き換えられています。  
  
 Pkgdef ファイルは、%localappdata%\Microsoft\Visual Studio\14.0\Extensions\ または%vsinstalldir%\Common7\IDE\Extensions のいずれかの場所にインストールする必要があり \\ ます。 インストールフォルダーが%localappdata%\Microsoft\Visual Studio\14.0\Extensions の場合、 \\ 拡張機能は Visual Studio によって認識されますが、既定では無効になります。 ユーザーは、 **拡張機能と更新プログラム**を使用して拡張機能を有効にすることができます。 インストールフォルダーが%vsinstalldir%\Common7\IDE\Extensions の場合 \\ 、拡張機能は既定で有効になっています。  
  
> [!NOTE]
> 拡張機能 **と更新プログラム** ツールは、VSIX パッケージの一部としてインストールされている場合を除き、拡張機能にアクセスするためには使用できません。  
  
## <a name="see-also"></a>参照  
 [CreateExpInstance ユーティリティ](../../extensibility/internals/createexpinstance-utility.md)
