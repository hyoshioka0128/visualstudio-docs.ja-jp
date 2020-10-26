---
title: カスタムデバッグエンジンの登録 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debug engines, registering
ms.assetid: 9984cd3d-d34f-4662-9ace-31766499abf5
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 9cf06e881034b980b8e40e095779007b3c7fa6f6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65703599"
---
# <a name="registering-a-custom-debug-engine"></a>カスタム デバッグ エンジンの登録
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

デバッグエンジンは、COM 規則に従うクラスファクトリとして自身を登録し、visual studio レジストリサブキーを使用して Visual Studio に登録する必要があります。  
  
> [!NOTE]
> デバッグエンジンを登録する方法の例については、 [「チュートリアル: ATL COM を使用したデバッグエンジンの構築](https://msdn.microsoft.com/9097b71e-1fe7-48f7-bc00-009e25940c24)」の一部として構築されている textinterpreter サンプルを参照してください。  
  
## <a name="dll-server-process"></a>DLL サーバープロセス  
 通常、デバッグエンジンは、COM サーバーとして独自の DLL に実装されます。 これは、Visual Studio がアクセスする前に、デバッグエンジンがそのクラスファクトリの CLSID を COM に登録する必要があることを意味します。 デバッグエンジンでサポートされているプロパティ (メトリックとも呼ばれます) を確立するには、デバッグエンジンがそれ自体を Visual Studio 自体に登録する必要があります。 デバッグエンジン用に Visual Studio レジストリサブキーに書き込まれるメトリックの選択は、デバッグエンジンがサポートする機能によって異なります。  
  
 [デバッグ用の SDK ヘルパー](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md) については、デバッグエンジンの登録に必要なレジストリの場所だけでなく、また、dbgmetric .lib ライブラリについても説明します。これには、レジストリの操作を容易にする C++ 開発者向けの便利な関数と宣言が多数含まれています。  
  
### <a name="example"></a>例  
 `SetMetric`関数 (dbgmetric) を使用して Visual Studio にデバッグエンジンを登録する方法を示す一般的な例 (TextInterpreter のサンプル) を次に示します。 渡されるメトリックは、dbgmetric. lib でも定義されています。  
  
> [!NOTE]
> TextInterpreter は基本的なデバッグエンジンです。その他の機能は実装されていないため、登録されません。 デバッグエンジンの完全な一覧に `SetMetric` は、デバッグエンジンがサポートしている機能ごとに1つずつ、呼び出しのリスト全体が含まれます。  
  
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
  
## <a name="see-also"></a>参照  
 [カスタムデバッグエンジンの作成](../../extensibility/debugger/creating-a-custom-debug-engine.md)   
 [デバッグ用の SDK ヘルパー](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)   
 [チュートリアル: ATL COM を使用したデバッグエンジンの構築](https://msdn.microsoft.com/9097b71e-1fe7-48f7-bc00-009e25940c24)
