---
title: コード化された UI テストでの HTML5 コントロールの使用
ms.date: 11/04/2016
ms.topic: conceptual
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: 13f5da784a43df5146a66ca868bb6add9a702906
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75585588"
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

|アクション|記録|生成されたコード|
|-|---------------|-|
|**オーディオの再生**<br /><br /> コントロールから直接、またはコントロールの右クリック メニューから。|\<name> オーディオを 00:00:00 の時点から再生|HtmlAudio.Play(TimeSpan)|
|**オーディオの特定の時点にシーク**|\<name> オーディオの 00:01:48 の時点にシーク|HtmlAudio.Seek(TimeSpan)|
|**オーディオの一時停止**<br /><br /> コントロールから直接、またはコントロールの右クリック メニューから。|\<name> オーディオの 00:01:53 の時点で一時停止|HtmlAudio.Pause(TimeSpan)|
|**オーディオのミュート**<br /><br /> コントロールから直接、またはコントロールの右クリック メニューから。|\<name> オーディオをミュート|HtmlAudio.Mute()|
|**オーディオのミュートの解除**<br /><br /> コントロールから直接、またはコントロールの右クリック メニューから。|\<name> オーディオのミュートを解除|HtmlAudio.Unmute()|
|**オーディオの音量の変更**|\<name> オーディオのボリュームを 79% に設定|HtmlAudio.SetVolume(float)|

アサーションを追加できるプロパティの一連については、「[HTMLAudioElement](https://developer.mozilla.org/docs/Web/API/HTMLAudioElement)」をご覧ください。

**検索プロパティ:** `HtmlAudio` の検索プロパティは、`Id`、`Name`、`Title` です。

**フィルター プロパティ:** `HtmlAudio` のフィルター プロパティは、`Src`、`Class`、`ControlDefinition`、`TagInstance` です。

> [!NOTE]
> Seek および Pause の時間は大きな意味を持つことがあります。 再生中、コード化された UI テストは、オーディオを一時停止する前に、`(TimeSpan)` に指定された時間まで待機します。 特殊な状況において、Pause コマンドが実行される前に指定された時間が経過したとき、例外がスローされます。

## <a name="video-control"></a>ビデオ コントロール
**ビデオ コントロール:** HTML5 ビデオ コントロールに対するアクションが正しく記録され再生されます。

![HTML5 ビデオ コントロール](../test/media/codedui_html5_video.png)

|アクション|記録|生成されたコード|
|-|---------------|-|
|**ビデオの再生**<br /><br /> コントロールから直接、またはコントロールの右クリック メニューから。|\<name> ビデオを 00:00:00 の時点から再生|HtmlVideo.Play(TimeSpan)|
|**ビデオの特定の時点にシーク**|\<name> ビデオの 00:01:48 の時点にシーク|HtmlVideo.Seek(TimeSpan)|
|**ビデオの一時停止**<br /><br /> コントロールから直接、またはコントロールの右クリック メニューから。|\<name> ビデオの 00:01:53 の時点で一時停止|HtmlVideo.Pause(TimeSpan)|
|**ビデオのミュート**<br /><br /> コントロールから直接、またはコントロールの右クリック メニューから。|\<name> ビデオをミュート|HtmlVideo.Mute()|
|**ビデオのミュートの解除**<br /><br /> コントロールから直接、またはコントロールの右クリック メニューから。|\<name> ビデオのミュートを解除|HtmlVideo.Unmute()|
|**ビデオの音量の変更**|\<name> ビデオのボリュームを 79% に設定||

アサーションを追加できるプロパティの一連については、「[HTMLVideoElement](https://developer.mozilla.org/docs/Web/HTML/Element/video)」をご覧ください。

**検索プロパティ:** `HtmlVideo` の検索プロパティは、`Id`、`Name`、`Title` です。

**フィルター プロパティ:** `HtmlVideo` のフィルター プロパティは、`Src`、`Poster`、`Class`、`ControlDefinition`、`TagInstance` です。

> [!NOTE]
> -30s または +30s のラベルを使用してビデオを巻き戻したり早送りしたりする場合、集計後の適切なタイミングにシークされます。

## <a name="progressbar"></a>ProgressBar
**ProgressBar コントロール:** ProgressBar は、非対話型コントロールです。 このコントロールの `Value` プロパティと `Max` プロパティでアサーションを追加できます。 詳しくは、「[HTMLProgressElement](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/progress)」をご覧ください。

![HTML5 ProgressBar コントロール](../test/media/codedui_html5_progressbar.png)

## <a name="see-also"></a>参照

- [HTML 要素](https://developer.mozilla.org/docs/Web/HTML/Element)
- [UI オートメーションを使用してコードをテストする](../test/use-ui-automation-to-test-your-code.md)
- [コード化された UI テストを作成する](../test/use-ui-automation-to-test-your-code.md)
- [コード化された UI テストと操作の記録でサポートされている構成とプラットフォーム](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)
