---
title: Iwefデバッグサポートインターフェイス
description: Visual Studio などのデバッグ環境を使用して Microsoft Office アプリケーションのデバッグを容易にする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: interface
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 6a818973bdc2f62194d6ed0026c0798806fe5f2a
ms.sourcegitcommit: 4bd2b770e60965fc0843fc25318a7e1b46137875
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/15/2020
ms.locfileid: "97525325"
---
# <a name="iwefdebuggingsupport-interface"></a>Iwefデバッグサポートインターフェイス
  Office 用アプリのデバッグを容易にするために、Visual Studio などのデバッグ環境によって実装されます。 Word や Excel などの Office アプリケーションは、Visual Studio からこのインターフェイスを取得し、デバッグセッション中に特定の時点でインターフェイスのメソッドを呼び出します。

## <a name="syntax"></a>構文

```csharp
[
    uuid(ccaf1a90-ce1c-4199-9cd6-b40c5c57a671),
    oleautomation
]
interface IWefDebuggingSupport : IUnknown
{
    HRESULT SetWefProcessId(
        [in] DWORD dwProcessId);
    HRESULT GetAutoInsertExtensions(
        [out, retval] SAFEARRAY(BSTR)* psaExtensionNames);
}
```

## <a name="methods"></a>メソッド
 次の表は、Iwefデバッグサポートインターフェイスで定義されるメソッドを示しています。

|名前|説明|
|----------|-----------------|
|[GetAutoInsertExtensions メソッド](../vsto/getautoinsertextensions-method.md)|デバッグ中に自動的に挿入される Office 用アプリに関する情報を取得します。|
|[SetWefProcessId メソッド](../vsto/setwefprocessid-method.md)|Web Extensions Framework (WEF) コンテンツを実行するプロセス識別子を提供します。|
