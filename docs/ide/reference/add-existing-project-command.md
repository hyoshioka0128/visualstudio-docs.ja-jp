---
title: AddExistingProject コマンド
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- file.addexistingproject
helpviewer_keywords:
- Add Existing Project command
- File.AddExistingProject
ms.assetid: 71cf3e31-c76b-405b-ad6a-1b1bc654bd40
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 008802546d87bd44137c6d13ee2aef802877e308
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75595879"
---
# <a name="add-existing-project-command"></a>AddExistingProject コマンド
既存のプロジェクトを現在のソリューションに追加します。

## <a name="syntax"></a>構文

```cmd
File.AddExistingProject filename
```

## <a name="arguments"></a>引数
`filename`\
任意。 ソリューションに追加するプロジェクトの完全なパスとプロジェクト名 (拡張子付き)。

`filename` 引数にスペースが含まれる場合は、引用符で囲む必要があります。

ファイル名が指定されていない場合、ファイルを開くダイアログ ボックスが表示され、ユーザーがプロジェクトを選択できます。

## <a name="remarks"></a>解説
オート コンプリートでは、入力された正しいパスとファイル名の検索を試みます。

## <a name="example"></a>例
この例では、[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] プロジェクトの TestProject1 を現在のソリューションに追加します。

```cmd
>File.AddExistingProject "c:\visual studio projects\TestProject1.vbproj"
```

## <a name="see-also"></a>参照

- [Visual Studio のコマンド](../../ide/reference/visual-studio-commands.md)
- [[コマンド] ウィンドウ](../../ide/reference/command-window.md)
- [検索コマンド ボックス](../../ide/find-command-box.md)
- [Visual Studio コマンドのエイリアス](../../ide/reference/visual-studio-command-aliases.md)
