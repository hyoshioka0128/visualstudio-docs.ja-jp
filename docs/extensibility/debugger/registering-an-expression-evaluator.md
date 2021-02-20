---
title: 式エバリュエーターの登録 |Microsoft Docs
description: 式エバリュエーターが、Windows COM 環境と Visual Studio の両方を備えたクラスファクトリとして自身を登録する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluators, registering
ms.assetid: 236be234-e05f-4ad8-9200-24ce51768ecf
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1074e8dea5dfdb05571d3b1aa04e5c411530bb1f
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99961106"
---
# <a name="register-an-expression-evaluator"></a>式エバリュエーターの登録
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 式エバリュエーター (EE) は、それ自体を Windows COM 環境と Visual Studio の両方を備えたクラスファクトリとして登録する必要があります。 EE は DLL として設定されるため、EE をインスタンス化するエンティティに応じて、デバッグエンジン (DE) アドレス空間または Visual Studio アドレス空間のいずれかに挿入されます。

## <a name="managed-code-expression-evaluator"></a>マネージコード式エバリュエーター
 マネージコード EE はクラスライブラリとして実装されます。これは、通常は VSIP プログラムの呼び出しによって開始される COM 環境にそれ自体を登録する DLL です。 *regpkg.exe* です。 COM 環境のレジストリキーを書き込む実際のプロセスは、自動的に処理されます。

 Main クラスのメソッドはでマークされ <xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute> ます。これは、DLL が COM に登録されているときにメソッドが呼び出されることを示します。 この登録方法は、多く `RegisterClass` の場合、Visual Studio に DLL を登録するタスクを実行します。 対応する `UnregisterClass` (でマークされた <xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute> ) `RegisterClass` 。 DLL がアンインストールされたときの効果を元に戻します。
アンマネージコードで記述された EE の場合と同じレジストリエントリが作成されます。唯一の違いは、作業を行うためのなどのヘルパー関数がないことです `SetEEMetric` 。 登録と登録解除のプロセスの例を次に示します。

### <a name="example"></a>例
 次の関数は、マネージコード EE が Visual Studio を使用して自身を登録および登録解除する方法を示しています。

```csharp
namespace EEMC
{
    [GuidAttribute("462D4A3D-B257-4AEE-97CD-5918C7531757")]
    public class EEMCClass : IDebugExpressionEvaluator
    {
        #region Register and unregister.
        private static Guid guidMycLang = new Guid("462D4A3E-B257-4AEE-97CD-5918C7531757");
        private static string languageName = "MyC";
        private static string eeName = "MyC Expression Evaluator";

        private static Guid guidMicrosoftVendor = new Guid("994B45C4-E6E9-11D2-903F-00C04FA302A1");
        private static Guid guidCOMPlusOnlyEng = new Guid("449EC4CC-30D2-4032-9256-EE18EB41B62B");
        private static Guid guidCOMPlusNativeEng = new Guid("92EF0900-2251-11D2-B72E-0000F87572EF");

        /// <summary>
        /// Register the expression evaluator.
        /// Set "project properties/configuration properties/build/register for COM interop" to true.
        /// </summary>
         [ComRegisterFunctionAttribute]
        public static void RegisterClass(Type t)
        {
            // Get Visual Studio version (set by regpkg.exe)
            string hive = Environment.GetEnvironmentVariable("EnvSdk_RegKey");
            string s = @"SOFTWARE\Microsoft\VisualStudio\"
                        + hive
                        + @"\AD7Metrics\ExpressionEvaluator";

            RegistryKey rk = Registry.LocalMachine.CreateSubKey(s);
            if (rk == null)  return;

            rk = rk.CreateSubKey(guidMycLang.ToString("B"));
            rk = rk.CreateSubKey(guidMicrosoftVendor.ToString("B"));
            rk.SetValue("CLSID", t.GUID.ToString("B"));
            rk.SetValue("Language", languageName);
            rk.SetValue("Name", eeName);

            rk = rk.CreateSubKey("Engine");
            rk.SetValue("0", guidCOMPlusOnlyEng.ToString("B"));
            rk.SetValue("1", guidCOMPlusNativeEng.ToString("B"));
        }
        /// <summary>
        /// Unregister the expression evaluator.
        /// </summary>
         [ComUnregisterFunctionAttribute]
        public static void UnregisterClass(Type t)
        {
            // Get Visual Studio version (set by regpkg.exe)
            string hive = Environment.GetEnvironmentVariable("EnvSdk_RegKey");
            string s = @"SOFTWARE\Microsoft\VisualStudio\"
                        + hive
                        + @"\AD7Metrics\ExpressionEvaluator\"
                        + guidMycLang.ToString("B");
            RegistryKey key = Registry.LocalMachine.OpenSubKey(s);
            if (key != null)
            {
                key.Close();
                Registry.LocalMachine.DeleteSubKeyTree(s);
            }
        }
    }
}
```

## <a name="unmanaged-code-expression-evaluator"></a>アンマネージコード式エバリュエーター
 EE DLL は、 `DllRegisterServer` Visual Studio だけでなく COM 環境にも登録する関数を実装しています。

> [!NOTE]
> MyCEE コードサンプルレジストリコードは、EnVSDK\MyCPkgs\MyCEE. の下にある VSIP インストールにあるファイル *dllentry. .cpp で見つかります。*

### <a name="dll-server-process"></a>DLL サーバープロセス
 EE を登録すると、DLL サーバーは次のようになります。

1. 通常の COM 規約に従って、クラスファクトリ `CLSID` を登録します。

2. ヘルパー関数を呼び出して、 `SetEEMetric` 次の表に示す EE メトリックを Visual Studio に登録します。 次のように `SetEEMetric` 指定された関数とメトリックは、 *dbgmetric .lib* ライブラリの一部です。 詳細については、「 [デバッグ用の SDK ヘルパー](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md) 」を参照してください。

    |メトリック|説明|
    |------------|-----------------|
    |`metricCLSID`|`CLSID` (EE クラスファクトリの)|
    |`metricName`|EE の名前を、任意の文字列として指定します。|
    |`metricLanguage`|EE が評価するように設計されている言語の名前|
    |`metricEngine`|`GUID`この EE で動作するデバッグエンジン (DE) の s|

    > [!NOTE]
    > では、 `metricLanguage``GUID` 言語が名前で識別されますが、の引数によって言語が選択され `guidLang` `SetEEMetric` ます。 コンパイラは、デバッグ情報ファイルを生成するときに、 `guidLang` 使用する EE を認識しないように適切なを記述する必要があります。 通常、DE はシンボルプロバイダーにこの言語を要求します。この言語は `GUID` デバッグ情報ファイルに格納されます。

3. HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudioの x. Y の下にキーを作成して Visual Studio に登録 \\ します。ここで、 *x.y* は、に登録する Visual Studio のバージョンです。

### <a name="example"></a>例
 次の関数は、アンマネージコード (C++) EE が Visual Studio でそれ自体を登録および登録解除する方法を示しています。

```cpp
/*---------------------------------------------------------
  Registration
-----------------------------------------------------------*/
#ifndef LREGKEY_VISUALSTUDIOROOT
    #define LREGKEY_VISUALSTUDIOROOT L"Software\\Microsoft\\VisualStudio\\8.0"
#endif

static HRESULT RegisterMetric( bool registerIt )
{
    // check where we should register
    const ULONG cchBuffer = _MAX_PATH;
    WCHAR wszRegistrationRoot[cchBuffer];
    DWORD cchFreeBuffer = cchBuffer - 1;
    wcscpy(wszRegistrationRoot, LREGKEY_VISUALSTUDIOROOT_NOVERSION);
    wcscat(wszRegistrationRoot, L"\\");

    // this is Environment SDK specific
    // we check for  EnvSdk_RegKey environment variable to
    // determine where to register
    DWORD cchDefRegRoot = lstrlenW(LREGKEY_VISUALSTUDIOROOT_NOVERSION) + 1;
    cchFreeBuffer = cchFreeBuffer - cchDefRegRoot;
    DWORD cchEnvVarRead = GetEnvironmentVariableW(
        /* LPCTSTR */ L"EnvSdk_RegKey", // environment variable name
        /* LPTSTR  */ &wszRegistrationRoot[cchDefRegRoot],// buffer for variable value
        /* DWORD   */ cchFreeBuffer);// size of buffer
    if (cchEnvVarRead >= cchFreeBuffer)
        return E_UNEXPECTED;
    // If the environment variable does not exist then we must use
    // LREGKEY_VISUALSTUDIOROOT which has the version number.
    if (0 == cchEnvVarRead)
        wcscpy(wszRegistrationRoot, LREGKEY_VISUALSTUDIOROOT);

    if (registerIt)
    {
        SetEEMetric(guidMycLang,
                    guidMicrosoftVendor,
                    metricCLSID,
                    CLSID_MycEE,
                    wszRegistrationRoot );
        SetEEMetric(guidMycLang,
                    guidMicrosoftVendor,
                    metricName,
                    GetString(IDS_INFO_MYCDESCRIPTION),
                    wszRegistrationRoot );
        SetEEMetric(guidMycLang,
                    guidMicrosoftVendor,
                    metricLanguage, L"MyC",
                    wszRegistrationRoot);

        GUID engineGuids[2];
        engineGuids[0] = guidCOMPlusOnlyEng;
        engineGuids[1] = guidCOMPlusNativeEng;
        SetEEMetric(guidMycLang,
                    guidMicrosoftVendor,
                    metricEngine,
                    engineGuids,
                    2,
                    wszRegistrationRoot);
    }
    else
    {
        RemoveEEMetric( guidMycLang,
                        guidMicrosoftVendor,
                        metricCLSID,
                        wszRegistrationRoot);
        RemoveEEMetric( guidMycLang,
                        guidMicrosoftVendor,
                        metricName,
                        wszRegistrationRoot );
        RemoveEEMetric( guidMycLang,
                        guidMicrosoftVendor,
                        metricLanguage,
                        wszRegistrationRoot );
        RemoveEEMetric( guidMycLang,
                        guidMicrosoftVendor,
                        metricEngine,
                        wszRegistrationRoot );
    }

    return S_OK;
}
```

## <a name="see-also"></a>関連項目
- [CLR 式エバリュエーターの記述](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
- [デバッグ用の SDK ヘルパー](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
