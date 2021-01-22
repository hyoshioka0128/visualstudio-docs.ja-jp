---
title: CommentMarkProfile | Microsoft Docs
description: CommentMarkProfile 関数を使用して、数字マーカーとテキスト文字列を *.vsp* ファイルに挿入します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- CommentMarkProfile
- CommentMarkProfileA
ms.assetid: 33ccff45-c33a-4672-b41f-5b317b848cd1
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: e943be08ffd586347ab5de54cb803bcedc8c24d7
ms.sourcegitcommit: 7a5c4f60667b5792f876953d55192b49a73f5fe9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2021
ms.locfileid: "98533590"
---
# <a name="commentmarkprofile"></a>CommentMarkProfile
`CommentMarkProfile` 関数は、 *.vsp* ファイルに数字マーカーとテキスト文字列を挿入します。 マークやコメントを挿入するには、`CommentMarkProfile` 関数が含まれるスレッドのプロファイリングをオンにする必要があります。

## <a name="syntax"></a>構文

```cpp
PROFILE_COMMAND_STATUS PROFILERAPI CommentMarkProfile(
                                   long lMarker,
                                   LPCTSTR szComment);
```

#### <a name="parameters"></a>パラメーター
 `lMarker`

 挿入する数字マーカー。 マーカーは 0 以上の値にする必要があります。

 `szComment`

 挿入するテキスト文字列のポインター。 文字列は、NULL 終端文字も含めて 256 文字位内にする必要があります。

## <a name="property-valuereturn-value"></a>プロパティ値/戻り値
 関数の成功または失敗は、**PROFILE_COMMAND_STATUS** 列挙型を使って表されます。 戻り値は次のいずれかになります。

|列挙子|説明|
|----------------|-----------------|
|MARK_ERROR_MARKER_RESERVED|パラメーターは 0 以下です。 これらの値は予約済みです。 マークとコメントは記録されません。|
|MARK_ERROR_MODE_NEVER|関数が呼び出されたときに、プロファイル モードが NEVER に設定されました。 マークとコメントは記録されません。|
|MARK_ERROR_MODE_OFF|関数が呼び出されたときに、プロファイル モードが OFF に設定されました。 マークとコメントは記録されません。|
|MARK_ERROR_NO_SUPPORT|このコンテキストでマークがサポートされていません。 マークとコメントは記録されません。|
|MARK_ERROR_OUTOFMEMORY|メモリ不足のため、このイベントを記録できません。 マークとコメントは記録されません。|
|MARK_TEXTTOOLONG|文字列の長さが最大値の 256 文字を超えています。 コメント文字列は切り詰められ、マークとコメントが記録されます。|
|MARK_OK|成功した場合は MARK_OK が返されます。|

## <a name="remarks"></a>Remarks
 Mark コマンドまたは関数 (CommentMarkAtProfile、CommentMarkProfile、MarkProfile) で VSInstr マークとコメントが挿入されたとき、マークのプロファイル関数を含むスレッドでは、プロファイル状態をオンにする必要があります。

 プロファイル マークは、スコープ内でグローバルです。 たとえば、あるスレッドに挿入したプロファイル マークを、 *.vsp* ファイル内の任意のスレッドで使用し、データ セグメントの開始または終了をマークできます。

> [!IMPORTANT]
> CommentMarkProfile メソッドはインストルメンテーションとの併用でのみ利用できます。

## <a name="net-framework-equivalent"></a>同等の .NET Framework 関数
 Microsoft.VisualStudio.Profiler.dll

## <a name="function-information"></a>関数の情報

|アイテム|[値]|
|-|-|
|**Header**|VSPerf.h をインクルードします。|
|**Library**|VSPerf.lib を使用します。|
|**Unicode**|`CommentMarkProfileW` (Unicode) および `CommentMarkProfileA` (ANSI) として実装します。|

## <a name="example"></a>例
 次のコードは、CommentMarkProfile 関数の呼び出しの例です。 この例では、コードで [!INCLUDE[vcpransi](../profiling/includes/vcpransi_md.md)] 関数を呼び出すかどうかを判断するために、Win32 文字列マクロと Unicode のコンパイラ設定が使用されていることを前提としています。

```cpp
void ExerciseCommentMarkProfile()
{
    // Declare and initalize variables to pass to
    // CommentMarkProfile.  The values of these
    // parameters are assigned based on the needs
    // of the code; and for the sake of simplicity
    // in this example, the variables are assigned
    // arbitrary values.
    long markId = 01;
    TCHAR * markText = TEXT("Exercising CommentMarkProfile...");

    // Variables used to print output.
    HRESULT hResult;
    TCHAR tchBuffer[256];

    // Declare MarkOperationResult Enumerator.
    // Holds return value from call to CommentMarkProfile.
    PROFILE_COMMAND_STATUS markResult;

    markResult = CommentMarkProfile(
        markId,
        markText);

    // Format and print result.
    LPCTSTR pszFormat = TEXT("%s %d.\0");
    TCHAR* pszTxt = TEXT("CommentMarkProfile returned");
    hResult = StringCchPrintf(tchBuffer, 256, pszFormat,
        pszTxt, markResult);

#ifdef DEBUG
    OutputDebugString(tchBuffer);
#endif
}
```

## <a name="see-also"></a>関連項目
- [Visual Studio プロファイラー API リファレンス (ネイティブ)](../profiling/visual-studio-profiler-api-reference-native.md)
