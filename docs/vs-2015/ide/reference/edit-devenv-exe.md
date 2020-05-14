---
title: -Edit (devenv.exe) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- Devenv, /edit switch
- /Edit Devenv swtich
ms.assetid: 02b3d6e7-a2b1-4d83-a747-aa8c2fb758b7
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: c81f59f2dadf535af4e9a76949a29fd1355c33f3
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72657745"
---
# <a name="edit-devenvexe"></a>/Edit (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

指定されたファイルを [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] の既存のインスタンスで開きます。

## <a name="syntax"></a>構文

```
Devenv /edit [file1[ file2]]
```

## <a name="arguments"></a>引数
 `file1` 省略可能。 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] の既存のインスタンスで開くファイル。 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] のインスタンスが存在していない場合は、簡略化されたウィンドウ レイアウトで新しいインスタンスが作成され、新しいインスタンスで `file1` が開かれます。

 `file2` 省略可能。 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] の既存インスタンスで開く 1 つ以上の追加ファイル。

## <a name="remarks"></a>解説
 ファイルが指定されておらず、[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] の既存のインスタンスがある場合は、[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] の既存のインスタンスがフォーカスを取得します。 ファイルが指定されておらず、[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] の既存のインスタンスがない場合は、[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] の新しいインスタンスが簡略化されたウィンドウ レイアウトで作成されます。

 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] の既存のインスタンスがモーダル状態の場合 (たとえば、[[オプション] ダイアログ ボックス](../../ide/reference/options-dialog-box-visual-studio.md)が開かれている場合)、[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] がモーダル状態を終了すると、ファイルが既存のインスタンスで開かれます。

## <a name="example"></a>例
 この例では、ファイル `MyFile.cs` が [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] の既存インスタンスで開かれるか、またはインスタンスがまだ存在しない場合は [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] の新しいインスタンスでファイルが開かれます。

```
devenv /edit MyFile.cs
```

## <a name="see-also"></a>関連項目
 [Devenv コマンド ライン スイッチ](../../ide/reference/devenv-command-line-switches.md)
