---
title: コード化された UI テストでの HTML5 コントロールの使用
description: Internet Explorer 9 および Internet Explorer 10 に含まれる HTML5 コントロールに対するコード化された UI テストのサポートについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: d902d31b0d417c32b7b3e1a2067a8bb5bcf77451
ms.sourcegitcommit: d6207a3a590c9ea84e3b25981d39933ad5f19ea3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/24/2020
ms.locfileid: "95598381"
---
# <a name="using-html5-controls-in-coded-ui-tests"></a>コード化された UI テストでの HTML5 コントロールの使用

コード化された UI テストには、Internet Explorer 9 と Internet Explorer 10 に含まれる HTML5 コントロールの一部のサポートが含まれます。

[!INCLUDE [coded-ui-test-deprecation](includes/coded-ui-test-deprecation.md)]

**必要条件**

- Visual Studio Enterprise

> [!WARNING]
> Internet Explorer 10 以前のバージョンでは、Internet Explorer プロセスより高い特権レベルでコード化された UI テストを実行できました。 Internet Explorer 10 でコード化された UI テストを実行するときは、コード化された UI テストと Internet Explorer のプロセスを同じ特権レベルで実行する必要があります。 これは、Internet Explorer 10 のよりセキュリティ レベルの高い AppContainer 機能によるものです。

> [!WARNING]
> Internet Explorer 10 でコード化された UI テストを作成した場合、そのテストは Internet Explorer 9 または Internet Explorer 8 を使用して実行できないことがあります。 これは、Internet Explorer 10 には、オーディオ、ビデオ、ProgressBar、スライダーなどの HTML5 コントロールが含まれているためです。 これらの HTML5 コントロールは、Internet Explorer 9 または Internet Explorer 8 で認識されません。 同様に、Internet Explorer 9 を使用するコード化された UI テストには、Internet Explorer 8 で認識されない HTML5 コントロールが含まれる場合があります。

## <a name="audio-control"></a>オーディオ コントロール

**オーディオ コントロール:** HTML5 オーディオ コントロールに対するアクションが正しく記録され再生されます。

![HTML5 オーディオ コントロール](../test/media/codedui_html5_audio.png)

|アクション|記録中|生成されたコード|
|-|---------------|-|
|**オーディオの再生**<br /><br /> コントロールから直接、またはコントロールの右クリック メニューから。|\<name> オーディオを 00:00:00 から再生する|HtmlAudio.Play(TimeSpan)|
|**オーディオの特定の時点にシーク**|\<name> オーディオを 00:01:48 にシークする|HtmlAudio.Seek(TimeSpan)|
|**オーディオの一時停止**<br /><br /> コントロールから直接、またはコントロールの右クリック メニューから。|\<name> オーディオを 00:01:53 で一時停止する|HtmlAudio.Pause(TimeSpan)|
|**オーディオのミュート**<br /><br /> コントロールから直接、またはコントロールの右クリック メニューから。|\<name> オーディオをミュートする|HtmlAudio.Mute()|
|**オーディオのミュートの解除**<br /><br /> コントロールから直接、またはコントロールの右クリック メニューから。|\<name> オーディオのミュートを解除する|HtmlAudio.Unmute()|
|**オーディオの音量の変更**|\<name> オーディオの音量を 79% に設定する|HtmlAudio.SetVolume(float)|

アサーションを追加できるプロパティの一連については、「[HTMLAudioElement](https://developer.mozilla.org/docs/Web/API/HTMLAudioElement)」をご覧ください。

**検索プロパティ:** `HtmlAudio` の検索プロパティは、`Id`、`Name`、`Title` です。

**フィルター プロパティ:** `HtmlAudio` のフィルター プロパティは、`Src`、`Class`、`ControlDefinition`、`TagInstance` です。

> [!NOTE]
> Seek および Pause の時間は大きな意味を持つことがあります。 再生中、コード化された UI テストは、オーディオを一時停止する前に、`(TimeSpan)` に指定された時間まで待機します。 特殊な状況において、Pause コマンドが実行される前に指定された時間が経過したとき、例外がスローされます。

## <a name="video-control"></a>ビデオ コントロール
**ビデオ コントロール:** HTML5 ビデオ コントロールに対するアクションが正しく記録され再生されます。

![HTML5 ビデオ コントロール](../test/media/codedui_html5_video.png)

|アクション|記録中|生成されたコード|
|-|---------------|-|
|**ビデオの再生**<br /><br /> コントロールから直接、またはコントロールの右クリック メニューから。|\<name> ビデオを 00:00:00 から再生する|HtmlVideo.Play(TimeSpan)|
|**ビデオの特定の時点にシーク**|\<name> ビデオを 00:01:48 にシークする|HtmlVideo.Seek(TimeSpan)|
|**ビデオの一時停止**<br /><br /> コントロールから直接、またはコントロールの右クリック メニューから。|\<name> ビデオを 00:01:53 で一時停止する|HtmlVideo.Pause(TimeSpan)|
|**ビデオのミュート**<br /><br /> コントロールから直接、またはコントロールの右クリック メニューから。|\<name> ビデオをミュートする|HtmlVideo.Mute()|
|**ビデオのミュートの解除**<br /><br /> コントロールから直接、またはコントロールの右クリック メニューから。|\<name> ビデオのミュートを解除する|HtmlVideo.Unmute()|
|**ビデオの音量の変更**|\<name> ビデオの音量を 79% に設定する||

アサーションを追加できるプロパティの一連については、「[HTMLVideoElement](https://developer.mozilla.org/docs/Web/HTML/Element/video)」をご覧ください。

**検索プロパティ:** `HtmlVideo` の検索プロパティは、`Id`、`Name`、`Title` です。

**フィルター プロパティ:** `HtmlVideo` のフィルター プロパティは、`Src`、`Poster`、`Class`、`ControlDefinition`、`TagInstance` です。

> [!NOTE]
> -30s または +30s のラベルを使用してビデオを巻き戻したり早送りしたりする場合、集計後の適切なタイミングにシークされます。

## <a name="progressbar"></a>ProgressBar
**ProgressBar コントロール:** ProgressBar は、非対話型コントロールです。 このコントロールの `Value` プロパティと `Max` プロパティでアサーションを追加できます。 詳しくは、「[HTMLProgressElement](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/progress)」をご覧ください。

![HTML5 ProgressBar コントロール](../test/media/codedui_html5_progressbar.png)

## <a name="see-also"></a>関連項目

- [HTML 要素](https://developer.mozilla.org/docs/Web/HTML/Element)
- [UI オートメーションを使用してコードをテストする](../test/use-ui-automation-to-test-your-code.md)
- [コード化された UI テストを作成する](../test/use-ui-automation-to-test-your-code.md)
- [コード化された UI テストと操作の記録でサポートされている構成とプラットフォーム](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)
