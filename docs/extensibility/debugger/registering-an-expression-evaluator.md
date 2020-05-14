---
title: 式エバリュエーターの登録 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluators, registering
ms.assetid: 236be234-e05f-4ad8-9200-24ce51768ecf
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 600f7c8a2e2957cddf23ccc82b0872617e491940
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80713204"
---
# <a name="register-an-expression-evaluator"></a>式エバリュエーターの登録
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターのこの実装方法は非推奨になりました。 CLR 式エバリュエーターの実装については[、「CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 」および「[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 式エバリュエーター (EE) は、Windows COM 環境と Visual Studio の両方にクラス ファクトリとして登録する必要があります。 EE は、EE をインスタンス化するエンティティに応じて、デバッグ エンジン (DE) アドレス空間または Visual Studio アドレス空間のいずれかに挿入されるように DLL として設定されます。

## <a name="managed-code-expression-evaluator"></a>マネージ コード式エバリュエーター
 マネージ コード EE はクラス ライブラリとして実装され、COM 環境に自身を登録する DLL であり、通常は VSIP プログラム*regpkg.exe*の呼び出しによって開始されます。 COM 環境のレジストリ キーを書き込む実際のプロセスは自動的に処理されます。

 メイン クラスのメソッドは、DLL<xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute>が COM に登録されるときに呼び出されることを示す 、 でマークされます。 この登録メソッドは、`RegisterClass`と呼ばれることが多いため、DLL を Visual Studio に登録するタスクを実行します。 対応する`UnregisterClass`( で<xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute>マーク ) は、DLL をアンインストールしたときの`RegisterClass`効果を元に行います。
アンマネージ コードで記述された EE と同じレジストリ エントリが作成されます。唯一の違いは、あなたのために作業を行うよう`SetEEMetric`なヘルパー関数が存在しないということです。 登録と登録解除のプロセスの例を次に示します。

### <a name="example"></a>例
 次の関数は、マネージ コード EE が Visual Studio に登録および登録解除する方法を示しています。

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

## <a name="unmanaged-code-expression-evaluator"></a>アンマネージ コード式エバリュエーター
 EE DLL は、Visual Studio だけでなく、COM 環境に自分自身を登録する`DllRegisterServer`関数を実装します。

> [!NOTE]
> MyCEE コード サンプルのレジストリ コードは、VSIP インストールの EnVSDK\MyCPkgs\MyCEE にある*dllentry.cpp*ファイルに含まれています。

### <a name="dll-server-process"></a>DLL サーバー プロセス
 EE を登録する際、DLL サーバは次の手順を実行します。

1. 通常の COM`CLSID`規則に従ってクラス ファクトリを登録します。

2. 次の表に`SetEEMetric`示す EE メトリックを Visual Studio に登録するヘルパー関数を呼び出します。 以下のように`SetEEMetric`指定される関数とメトリックは *、dbgmetric.lib*ライブラリーの一部です。 [詳細については、SDK ヘルパーを](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)参照してください。

    |メトリック|説明|
    |------------|-----------------|
    |`metricCLSID`|`CLSID`EEクラスの工場の|
    |`metricName`|表示可能な文字列としての EE の名前|
    |`metricLanguage`|EE が評価するように設計されている言語の名前|
    |`metricEngine`|`GUID`この EE で動作するデバッグ エンジン (DE) の s|

    > [!NOTE]
    > は`metricLanguage``GUID`、名前で言語を識別しますが、言語を`guidLang`選択する`SetEEMetric`引数です。 コンパイラは、デバッグ情報ファイルを生成するときに、DE が使用する`guidLang`EE を認識するように適切な情報を書き込む必要があります。 通常、DE は、デバッグ情報ファイルに`GUID`格納されているこの言語のシンボル プロバイダーに要求します。

3. X.Y は登録する Visual Studio のバージョンであるHKEY_LOCAL_MACHINE\\\ソフトウェア\マイクロソフト\VisualStudio*X.Y*の下にキーを作成して、Visual Studio に登録します。 *X.Y*

### <a name="example"></a>例
 次の関数は、アンマネージ コード (C++) EE が Visual Studio に登録および登録解除する方法を示しています。

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
