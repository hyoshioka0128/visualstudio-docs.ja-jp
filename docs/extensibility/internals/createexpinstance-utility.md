---
title: インスタンスユーティリティを作成する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- experimental builds
- experimental hive
- experimental instance
- createexpinstance
- createexpinst
ms.assetid: 03779774-9401-49ae-997c-0c3ab25ed0d5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6a6b302976495e6067fad14317856cda4ac4625f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709242"
---
# <a name="createexpinstance-utility"></a>ユーティリティを作成します。
Visual Studio の実験用インスタンスを作成、リセット、または削除するには **、CreateExpInstance**ユーティリティを使用します。 実験用インスタンスを使用すると、基になる製品を変更することなく、Visual Studio 拡張機能をデバッグおよびテストできます。

## <a name="syntax"></a>構文

```
CreateExpInstance.exe [/Create | /Reset | /Clean] /VSInstance=VsInstance /RootSuffix=Suffix
```

## <a name="parameters"></a>パラメーター
 **/作成**実験用インスタンスを作成します。

 **/リセット**実験用インスタンスを削除し、新しいインスタンスを作成します。

 **/クリーン**実験用インスタンスを削除します。

 **/インスタンス**コピーする基本 Visual Studio インスタンスを含むディレクトリの名前。

 **/ルートサフィックス**実験用インスタンスディレクトリの名前に追加するサフィックス。

## <a name="remarks"></a>Remarks
 Visual Studio 拡張機能を使用している場合は、F5 キーを押して既定の実験用インスタンスを開き、現在の拡張機能をインストールできます。 使用できる実験用インスタンスがない場合、Visual Studio は既定の設定を持つインスタンスを作成します。

 実験用インスタンスの既定の場所は、Visual Studio のバージョン番号によって異なります。 たとえば、Visual Studio 2015 の場合、場所は *%localappdata%\Microsoft\VisualStudio\14.0Exp です\\*。 ディレクトリの場所にあるすべてのファイルは、そのインスタンスの一部と見なされます。 ディレクトリ名が既定の場所に変更されない限り、追加の実験用インスタンスは Visual Studio によって読み込まれません。

 実験用インスタンスを開くときに、Visual Studio はシステム レジストリにアクセスしません。 これは、レジストリ ハイブの実験用バージョンを使用した以前のバージョンの Visual Studio とは異なります。

 ユーティリティ**は****、VsRegEx**ユーティリティに置き換えられます。

 次の例では、Visual Studio の既定の実験用インスタンスをリセットします。

 **を設定 /リセット /VSインスタンス=14.0 /ルートサフィックス=Exp**

## <a name="see-also"></a>関連項目
- [VSPackages](../../extensibility/internals/vspackages.md)
