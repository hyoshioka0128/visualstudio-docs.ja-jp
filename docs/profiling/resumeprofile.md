---
title: ResumeProfile | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- ResumeProfile
ms.assetid: 876f145b-ec07-4240-ade6-4f6e44baadce
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 3d65d5fcf8961493c2b780453f2143de788551a5
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "74778311"
---
# <a name="resumeprofile"></a>ResumeProfile
`ResumeProfile` メソッドは、指定されたプロファイル レベルの保留/再開カウンターをデクリメントします。

## <a name="syntax"></a>構文

```cpp
PROFILE_COMMAND_STATUS PROFILERAPI ResumeProfile(
                       PROFILE_CONTROL_LEVEL Level,
                       unsigned int dwId);
```

#### <a name="parameters"></a>パラメーター
 `Level`

 パフォーマンス データ収集を適用できるプロファイル レベルを示します。 次の **PROFILE_CONTROL_LEVEL** 列挙子を使用して、パフォーマンス データ収集を適用できる 3 つのレベルのいずれかを示すことができます。

|列挙子|[説明]|
|----------------|-----------------|
|PROFILE_GLOBALLEVEL|グローバル レベル設定は、プロファイル実行のすべてのプロセスとスレッドに影響します。|
|PROFILE_PROCESSLEVEL|プロセス レベル設定は、指定されたプロセスの一部であるスレッドすべてに影響します。|
|PROFILE_THREADLEVEL|スレッド プロファイル レベル設定は、指定されたスレッドに影響します。|

 `dwId`

 システムによって生成される、プロセスまたはスレッドの ID。

## <a name="property-valuereturn-value"></a>プロパティ値/戻り値
 関数の成功または失敗は、**PROFILE_COMMAND_STATUS** 列挙型を使って表されます。 戻り値は次のいずれかになります。

|列挙子|[説明]|
|----------------|-----------------|
|PROFILE_ERROR_ID_NOEXIST|プロファイル要素 ID が存在しません。|
|PROFILE_ERROR_LEVEL_NOEXIST|指定されたプロファイル レベルが存在しません。|
|PROFILE_ERROR_MODE_NEVER|関数が呼び出されたときに、プロファイル モードが NEVER に設定されました。|
|PROFILE_ERROR_NOT_YET_IMPLEMENTED|プロファイル関数呼び出し、プロファイル レベル、または呼び出しとレベルの組み合わせがまだ実装されていません。|
|PROFILE_OK|呼び出しに成功しました。|

## <a name="remarks"></a>解説
 保留/再開カウンターの初期値は 0 です。 SuspendProfile を呼び出すたびに、保留/再開数に 1 が加算され、ResumeProfile を呼び出すたびに、1 が減算されます。

 保留/再開数が 0 よりも大きい場合、そのレベルの保留/再開状態はオフになります。 数が 0 以下の場合、保留/再開状態はオンになります。

 開始/停止状態と保留/再開状態の両方がオンの場合、そのレベルのプロファイル状態はオンです。 プロファイルの対象となるスレッドでは、グローバル、プロセス、およびスレッド レベル状態がすべてオンである必要があります。

## <a name="net-framework-equivalent"></a>同等の .NET Framework 関数
 *Microsoft.VisualStudio.Profiler.dll*

## <a name="function-information"></a>関数の情報
 ヘッダー : *VSPerf.h* で宣言

 インポート ライブラリ : *VSPerf.lib*

## <a name="example"></a>例
 ResumeProfile 関数の例を以下に示します。 この例は、[PROFILE_CURRENTID](../profiling/profile-currentid.md) で識別される同じスレッドまたはプロセスに対して、SuspendProfile メソッドが呼び出されていることを前提としています。

```cpp
void ExerciseResumeProfile()
{
    // The initial value of the Suspend/Resume counter is 0.
    // Each call to SuspendProfile adds 1 to the Suspend/Resume
    // count; each call to ResumeProfile subtracts 1.

    // Variables used to print output.
    HRESULT hResult;
    TCHAR tchBuffer[256];

    // Declare enumeration to hold result of call to ResumeProfile
    PROFILE_COMMAND_STATUS profileResult;

    profileResult = ResumeProfile(
        PROFILE_GLOBALLEVEL,
        PROFILE_CURRENTID);

    // Format and print result.
    LPCTSTR pszFormat = TEXT("%s %d.\0");
    TCHAR* pszTxt = TEXT("ResumeProfile returned");
    hResult = StringCchPrintf(tchBuffer, 256, pszFormat,
        pszTxt, profileResult);

#ifdef DEBUG
    OutputDebugString(tchBuffer);
#endif
}
```

## <a name="see-also"></a>参照
- [Visual Studio プロファイラー API リファレンス (ネイティブ)](../profiling/visual-studio-profiler-api-reference-native.md)
