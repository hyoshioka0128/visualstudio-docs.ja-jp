---
description: Visual Studio の設定をインポート、エクスポート、またはリセットします。
title: '[設定のインポートとエクスポート] コマンド'
ms.date: 11/21/2018
ms.topic: reference
f1_keywords:
- Tools.ImportandExportSettings
helpviewer_keywords:
- Tools.ImportandExportSettings
- Import and Export Settings command
ms.assetid: 94a06468-a44d-403d-a931-77bbc9d06e56
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0f2ea4811af2c44277b9a6dc285972c5267b28d7
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102223675"
---
# <a name="import-and-export-settings-command"></a>[設定のインポートとエクスポート] コマンド

Visual Studio の設定をインポート、エクスポート、またはリセットします。

## <a name="syntax"></a>構文

```cmd
Tools.ImportandExportSettings [/export:filename | /import:filename | /reset]
```

## <a name="switches"></a>スイッチ

/export:`filename`

任意。 現在の設定を指定したファイルにエクスポートします。

/import:`filename`

任意。 設定を指定したファイルからインポートします。

/reset

任意。 現在の設定をリセットします。

## <a name="remarks"></a>注釈

スイッチを指定しないでこのコマンドを実行すると、**[設定のインポートとエクスポート]** ウィザードが開きます。 詳細については、[設定の同期](../synchronized-settings-in-visual-studio.md)と[環境設定](../environment-settings.md)に関するページを参照してください。

## <a name="example"></a>例

次のコマンドは、現在の設定を `MyFile.vssettings` ファイルにエクスポートします。

```cmd
Tools.ImportandExportSettings /export:"c:\Files\MyFile.vssettings"
```

## <a name="see-also"></a>関連項目

- [環境設定](../../ide/environment-settings.md)
- [設定を同期する](../../ide/synchronized-settings-in-visual-studio.md)
- [Visual Studio IDE のカスタマイズ](../../ide/personalizing-the-visual-studio-ide.md)
- [Visual Studio コマンド](../../ide/reference/visual-studio-commands.md)
