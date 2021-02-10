---
title: カスタムデバッグエンジンの登録 |Microsoft Docs
description: デバッグエンジンが自身をクラスファクトリとして登録する方法、COM 規則に従う方法、およびレジストリを使用して Visual Studio に登録する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, registering
ms.assetid: 9984cd3d-d34f-4662-9ace-31766499abf5
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4581411a2601bf598762a7157f9df0e006995230
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99961119"
---
# <a name="register-a-custom-debug-engine"></a>カスタムデバッグエンジンを登録する
デバッグエンジンは、それ自体をクラスファクトリとして登録する必要があります。 COM の規則に従うだけでなく、visual studio のレジストリサブキーを使用して Visual Studio に登録する必要があります。

> [!NOTE]
> デバッグエンジンの登録方法の例については、 [「チュートリアル: ATL COM を使用したデバッグエンジンの構築](/previous-versions/bb147024(v=vs.90))」の一部として作成されている textinterpreter サンプルを参照してください。

## <a name="dll-server-process"></a>DLL サーバープロセス
 デバッグエンジンは、通常、独自の DLL で COM サーバーとして設定されます。 そのため、Visual Studio がアクセスできるようにするには、デバッグエンジンがそのクラスファクトリの CLSID を COM に登録する必要があります。 次に、デバッグエンジンは、デバッグエンジンがサポートしているすべてのプロパティ (メトリックとも呼ばれます) を確立するために、それ自体を Visual Studio に登録する必要があります。 Visual Studio レジストリサブキーに書き込まれるメトリックの選択は、デバッグエンジンがサポートする機能によって異なります。

 [デバッグ用の SDK ヘルパー](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md) については、デバッグエンジンの登録に必要なレジストリの場所だけでなく、また、 *dbgmetric .lib* ライブラリについても説明します。これには、レジストリの操作を容易にする C++ 開発者向けの便利な関数と宣言が多数含まれています。

### <a name="example"></a>例
 (TextInterpreter サンプルの) 次の例では、 `SetMetric` 関数 ( *dbgmetric*) を使用して、デバッグエンジンを Visual Studio に登録する方法を示しています。 渡されるメトリックは、 *dbgmetric. lib* でも定義されています。

> [!NOTE]
> TextInterpreter は基本的なデバッグエンジンです。その他の機能は設定されないため、登録されません。 デバッグエンジンの完全な一覧に `SetMetric` は、デバッグエンジンがサポートしている機能ごとに1つずつ、呼び出しのリスト全体が含まれます。

```
// Define base registry subkey to Visual Studio.
static const WCHAR strRegistrationRoot[] = L"Software\\Microsoft\\VisualStudio\\8.0";

HRESULT CTextInterpreterModule::RegisterServer(BOOL bRegTypeLib, const CLSID * pCLSID)
{
    SetMetric(metrictypeEngine, __uuidof(Engine), metricName, L"Text File", false, strRegistrationRoot);
    SetMetric(metrictypeEngine, __uuidof(Engine), metricCLSID, CLSID_Engine, false, strRegistrationRoot);
    SetMetric(metrictypeEngine, __uuidof(Engine), metricProgramProvider, CLSID_MsProgramProvider, false, strRegistrationRoot);

    return base::RegisterServer(bRegTypeLib, pCLSID);
}
```

## <a name="see-also"></a>関連項目
- [カスタムデバッグエンジンの作成](../../extensibility/debugger/creating-a-custom-debug-engine.md)
- [デバッグ用の SDK ヘルパー](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
- [チュートリアル: ATL COM を使用したデバッグエンジンの構築](/previous-versions/bb147024(v=vs.90))