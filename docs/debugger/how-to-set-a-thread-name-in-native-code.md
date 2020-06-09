---
title: '方法: ネイティブ コードのスレッド名を設定する | Microsoft Docs'
ms.date: 12/17/2018
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- debugging [C++], threads
- SetThreadName function
- threading [Visual Studio], names
- thread names
- debugging [Visual Studio], threads
ms.assetid: c85d0968-9f22-4d69-87f4-acca2ae777b8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: 1e719563c831c50cc325d70d0de431f4be1bf514
ms.sourcegitcommit: 257fc60eb01fefafa9185fca28727ded81b8bca9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72911425"
---
# <a name="how-to-set-a-thread-name-in-native-code"></a>方法: ネイティブ コードのスレッド名を設定する
スレッド名の設定は、Visual Studio のどのエディションでも実行できます。 スレッドの名前付けは、実行中のプロセスをデバッグするときに、 **[スレッド]** ウィンドウで対象のスレッドを識別するために役立ちます。 スレッドにわかりやすい名前を付けると、クラッシュ ダンプ検査を介して事後デバッグを実行するときや、さまざまなツールを使用してパフォーマンス キャプチャを分析するときにも役立ちます。

## <a name="ways-to-set-a-thread-name"></a>スレッド名を設定する方法

スレッド名を設定するには、2 つの方法があります。 1 つ目は、[SetThreadDescription](/windows/desktop/api/processthreadsapi/nf-processthreadsapi-setthreaddescription) 関数を使用する方法です。 2 つ目は、Visual Studio デバッガーがプロセスにアタッチされているときに特定の例外をスローする方法です。 それぞれのアプローチに利点と注意点があります。 `SetThreadDescription` の使用は、Windows 10 バージョン 1607 または Windows Server 2016 以降でサポートされています。

これらのメカニズムは互いに独立しているため、必要に応じて、"_両方_" のアプローチを同時に使用できる点が重要です。

### <a name="set-a-thread-name-by-using-setthreaddescription"></a>`SetThreadDescription` を使用してスレッド名を設定する

利点:
* スレッド名は、SetThreadDescription が呼び出されたときにデバッガーがプロセスにアタッチされていたかどうかに関係なく、Visual Studio でデバッグするときに表示されます。
* Visual Studio でクラッシュ ダンプを読み込んで事後デバッグを実行すると、スレッド名が表示されます。
* スレッド名は、[WinDbg](/windows-hardware/drivers/debugger/debugger-download-tools) デバッガーや [Windows パフォーマンス アナライザー](/windows-hardware/test/wpt/windows-performance-analyzer) パフォーマンス アナライザーなどの他のツールを使用しているときにも表示されます。

注意事項:
* スレッド名は、Visual Studio 2017 バージョン 15.6 以降のバージョンでのみ表示されます。
* クラッシュ ダンプ ファイルの事後デバッグでは、Windows 10 バージョン 1607、Windows Server 2016 以降のバージョンの Windows 上でクラッシュが発生した場合にのみ、スレッド名が表示されます。

*例:*

```C++
#include <windows.h>
#include <processthreadsapi.h>

int main()
{
    HRESULT r;
    r = SetThreadDescription(
        GetCurrentThread(),
        L"ThisIsMyThreadName!"
    );

    return 0;
}
```

### <a name="set-a-thread-name-by-throwing-an-exception"></a>例外をスローしてスレッド名を設定する

プログラムでスレッド名を設定するもう 1 つの方法は、特別に構成された例外をスローして、目的のスレッド名を Visual Studio デバッガーに通知することです。

利点:
* Visual Studio のすべてのバージョンで動作します。

注意事項:
* デバッガーがアタッチされ、例外ベースの方法が使用されている場合にのみ動作します。
* この方法を使用して設定されたスレッド名は、ダンプまたはパフォーマンス分析ツールでは使用できません。

*例:*

以下に示す `SetThreadName` 関数は、この例外ベースのアプローチを示しています。 スレッド名は自動的にスレッドにコピーされるので、`SetThreadName` の呼び出しが完了した後、`threadName` パラメーターのメモリを解放できることに注意します。

```C++
//
// Usage: SetThreadName ((DWORD)-1, "MainThread");
//
#include <windows.h>
const DWORD MS_VC_EXCEPTION = 0x406D1388;
#pragma pack(push,8)
typedef struct tagTHREADNAME_INFO
{
    DWORD dwType; // Must be 0x1000.
    LPCSTR szName; // Pointer to name (in user addr space).
    DWORD dwThreadID; // Thread ID (-1=caller thread).
    DWORD dwFlags; // Reserved for future use, must be zero.
} THREADNAME_INFO;
#pragma pack(pop)
void SetThreadName(DWORD dwThreadID, const char* threadName) {
    THREADNAME_INFO info;
    info.dwType = 0x1000;
    info.szName = threadName;
    info.dwThreadID = dwThreadID;
    info.dwFlags = 0;
#pragma warning(push)
#pragma warning(disable: 6320 6322)
    __try{
        RaiseException(MS_VC_EXCEPTION, 0, sizeof(info) / sizeof(ULONG_PTR), (ULONG_PTR*)&info);
    }
    __except (EXCEPTION_EXECUTE_HANDLER){
    }
#pragma warning(pop)
}
```

## <a name="see-also"></a>関連項目
- [マルチスレッド アプリケーションのデバッグ](../debugger/debug-multithreaded-applications-in-visual-studio.md)
- [デバッガーでのデータ表示](../debugger/viewing-data-in-the-debugger.md)
- [方法: マネージド コードのスレッド名を設定する](../debugger/how-to-set-a-thread-name-in-managed-code.md)
