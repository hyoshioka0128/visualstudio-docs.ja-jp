---
title: カスタム デバッグ エンジンを登録する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, registering
ms.assetid: 9984cd3d-d34f-4662-9ace-31766499abf5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fe6fb916810bc8a7e960a4723a6a7c7a6f0c1410
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80713224"
---
# <a name="register-a-custom-debug-engine"></a>カスタム デバッグ エンジンを登録する
デバッグ エンジンは、クラス ファクトリとして登録し、COM の規則に従って、Visual Studio レジストリ サブキーを使用して Visual Studio に登録する必要があります。

> [!NOTE]
> デバッグ エンジンを登録する方法の例を見つけることができます、 TextInterpreter のサンプルチュートリアルの一部として構築されている[、 ATL COM を使用してデバッグ エンジンを構築](https://msdn.microsoft.com/library/9097b71e-1fe7-48f7-bc00-009e25940c24)します。

## <a name="dll-server-process"></a>DLL サーバー プロセス
 デバッグ エンジンは、通常、COM サーバーとして独自の DLL にセットアップされます。 そのため、Visual Studio がアクセスできるようにするには、デバッグ エンジンはクラス ファクトリの CLSID を COM に登録する必要があります。 次に、デバッグ エンジンがサポートするプロパティ (メトリックと呼ばれます) を確立するために、デバッグ エンジン自体を Visual Studio に登録する必要があります。 Visual Studio レジストリ サブキーに書き込まれるメトリックの選択は、デバッグ エンジンがサポートする機能によって異なります。

 [デバッグ用の SDK ヘルパー](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)は、デバッグ エンジンの登録に必要なレジストリの場所だけでなく、デバッグ エンジンを登録する場合も説明します。また *、dbgmetric.lib*ライブラリについても説明します。

### <a name="example"></a>例
 次の例 (TextInterpreter サンプルから) は、`SetMetric`関数 *(dbgmetric.lib*から) を使用して Visual Studio にデバッグ エンジンを登録する方法を示しています。 渡されるメトリックは*dbgmetric.lib*でも定義されます。

> [!NOTE]
> TextInterpreter は基本的なデバッグ エンジンです。他の機能は設定されず、登録されません。 より完全なデバッグ エンジンは、呼び出`SetMetric`しの全体の一覧または同等のデバッグ エンジンがサポートする各機能に対して 1 つずつを持ちます。

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
- [カスタム デバッグ エンジンの作成](../../extensibility/debugger/creating-a-custom-debug-engine.md)
- [デバッグ用の SDK ヘルパー](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
- [チュートリアル: ATL COM を使用したデバッグ エンジンの作成](https://msdn.microsoft.com/library/9097b71e-1fe7-48f7-bc00-009e25940c24)
