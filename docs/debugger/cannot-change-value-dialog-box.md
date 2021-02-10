---
title: '[値を変更できません] ダイアログ ボックス | Microsoft Docs'
description: '[値を変更できません] ダイアログ ボックスについて説明します。これは、Visual Studio で、デバッガー ウィンドウまたは QuickWatch で変数を不正な値に変更しようとすると表示されます。'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.debug.variables.failededit
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Cannot Change Value dialog box
- variables [debugger], editing
ms.assetid: 19e930c2-5fbf-4c83-aae8-a1dc3f8fcae8
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 3dfedc12a1634e6f804c0cb3a9fceee9e9d43216
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99857891"
---
# <a name="cannot-change-value-dialog-box"></a>[値を変更できません] ダイアログ ボックス
## <a name="error"></a>Error
 `The value of this variable cannot be changed` &#124; `The name` *<名前>* `does not exist in the current context` &#124; *<その他のさまざまなメッセージ>*

 このメッセージ ボックスが表示されるのは、デバッガー ウィンドウ ([自動変数]、[ウォッチ]、または [ローカル] の各ウィンドウ)、または [クイック ウォッチ] ダイアログ ボックスで変数の内容を不正な値に変更しようとした場合です。 たとえば、整数値を文字列に設定しようとすると、このメッセージ ボックスが表示されます。

## <a name="solution"></a>ソリューション
 デバッグ用ウィンドウや [クイック ウォッチ] ダイアログ ボックスに入力した内容が、設定する変数に対して有効な値を表していることを確認します。

## <a name="see-also"></a>関連項目

- [デバッガー内の式](../debugger/expressions-in-the-debugger.md)