---
title: -ResetAddin (devenv.exe) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- disable addin
- addin state
- reset addin
ms.assetid: 9e339c8d-d768-4d86-8f45-2f479fc8255b
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 9958e6e9a540dce1a405df8991780600b8f4a702
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72665600"
---
# <a name="resetaddin-devenvexe"></a>/ResetAddin (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

コマンドおよび指定されたアドインに関連付けられたコマンド UI を削除します。

## <a name="syntax"></a>構文

```
Devenv /ResetAddin AddIn
```

## <a name="arguments"></a>引数
 `AddIn` 省略可能。 アドインのコマンド名。

## <a name="remarks"></a>解説
 既定では、アドインのコマンド名は *\<AddInSolutionName>* .Connect<em>.\<AddInSolutionName></em> と同じで、Connect.cs では `Exec` メソッドの `commandName` パラメーターとして表示されます。 また、Visual Studio のコマンド ウィンドウでアドインの名前を途中まで入力し、IntelliSense を使用して残りを自動的に表示させることでコマンド名を確認することもできます。

## <a name="example"></a>例
 次の例は、Visual Studio を起動して、`MyAddin` アドインを起動時に実行しないようにします。

```
Devenv.exe /ResetAddin MyAddin.Connect.MyAddin
```

## <a name="see-also"></a>関連項目
 Visual Studio [Devenv コマンドラインスイッチ](../../ide/reference/devenv-command-line-switches.md)[での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)
