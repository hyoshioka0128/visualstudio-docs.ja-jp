---
title: Windows API 関数をデバッグする |Microsoft Docs
ms.custom: seodec18
ms.date: 06/03/2020
ms.topic: how-to
f1_keywords:
- vs.debug.api
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [C++], Windows API functions
- NT symbols and debugging Windows API functions
- Windows API functions, debugging
- Windows API, debugging API functions
- APIs, debugging
ms.assetid: 7c126f57-62ab-4d94-9805-632d696ba1f0
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6fab5627f3d467c0df289969e4fee010dd3ea78b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85350395"
---
# <a name="how-can-i-debug-windows-api-functions"></a>Windows API 関数をデバッグするには
NT シンボルを読み込んだ状態で Windows API 関数をデバッグするには、次の手順を実行する必要があります。

### <a name="to-set-a-breakpoint-on-a-windows-api-function-with-nt-symbols-loaded"></a>NT シンボルを読み込んだ状態で Windows API 関数にブレークポイントを設定するには

- [関数のブレークポイント](../debugger/using-breakpoints.md#BKMK_Set_a_breakpoint_in_a_source_file)に、関数が存在する DLL の名前と共に関数名を入力します ([コンテキスト演算子](../debugger/context-operator-cpp.md)に関するページを参照してください)。 32 ビット コードでは、関数名の装飾形式を使用します。 たとえば、**MessageBeep** にブレークポイントを設定するには、次のように入力します。

    ```cpp
    {,,USER32.DLL}_MessageBeep@4
    ```

     装飾名を取得するには、「[装飾名の表示](https://msdn.microsoft.com/library/f79e2717-a4db-4d12-a689-69830cce2be0)」を参照してください 。

     装飾名をテストし、逆アセンブリ コードで表示できます。 Visual Studio デバッガーの関数で一時停止しているときに、コード エディターまたは呼び出し履歴ウィンドウで関数を右クリックし、 **[逆アセンブリへ移動]** を選択します。

- 64 ビット コードでは、非装飾名を使用できます。

    ```cpp
    {,,USER32.DLL}MessageBeep
    ```

## <a name="see-also"></a>関連項目
- [ネイティブ コードのデバッグに関する FAQ](../debugger/debugging-native-code-faqs.md)
- [ネイティブ コードのデバッグ](../debugger/debugging-native-code.md)
