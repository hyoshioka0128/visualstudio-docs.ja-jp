---
title: AI Tools をインストールする
description: AI Tools for Visual Studio をインストールする方法を説明します。
keywords: AI, Visual Studio
author: jillre
ms.author: jillfra
manager: jillfra
monikerRange: vs-2017
ms.date: 11/13/2017
ms.topic: conceptual
ms.workload:
- multiple
ms.openlocfilehash: ffa8c7634c0d97dd24ff69814ae73ad5ff12928b
ms.sourcegitcommit: a801ca3269274ce1de4f6b2c3f40b58bbaa3f460
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88800204"
---
# <a name="installation"></a>インストール

Visual Studio Tools for AI は、64 ビットの Windows オペレーティング システムにインストールできます。

## <a name="install-visual-studio-tools-for-ai"></a>Visual Studio Tools for AI のインストール

この拡張機能は、Visual Studio 2015 および Visual Studio 2017 の Community Edition 以上で動作します。

このツールは、[Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.vstoolsai-vs2017) または Visual Studio 内からダウンロードしてインストールします。

1. **[ツール]**  >  **[拡張機能と更新プログラム]** を選択します。

   ![Visual Studio の拡張機能と更新プログラム メニュー](media/installation/extensions.png)

2. **[拡張機能と更新プログラム]** ダイアログ ボックスで左側の **[オンライン]** を選択します。
3. 右上隅の検索ボックスに「tools for ai」と入力します。
4. 結果から、「**Visual Studio Tools for AI**」を選択します。
5. **[ダウンロード]** を選択します。

## <a name="prepare-your-local-machine"></a>ローカル コンピューターを準備する
ローカル コンピューター上でディープ ラーニング モデルをトレーニングする前に、該当する前提条件がインストールされていることを確認する必要があります。 これには、NVIDIA GPU (お持ちの場合) の最新のドライバーとライブラリの所持の確認が含まれます。 また、Python と Python ライブラリ (NumPy、SciPy など)、およびプロジェクトで使う予定の適切なディープ ラーニング フレームワーク (Microsoft Cognitive Toolkit (CNTK)、TensorFlow、Caffe2、MXNet、Keras、Theano、PyTorch、Chainer など) がインストールされていることを確認します。

> [!NOTE]
> 以下のソフトウェアの概要は、これらのホーム ページからの抜粋です。

### <a name="nvidia-gpu-driver"></a>NVIDIA GPU ドライバー

ディープ ラーニング フレームワークは、NVIDIA GPU を利用して、真の人工知能に向けたマシンによる高速、正確、大規模な学習を可能にします。 コンピューターに NVIDIA GPU のカードがある場合は、「[NVIDIA ドライバーのダウンロード](https://www.nvidia.com/Download/index.aspx)」を参照するか、またはオペレーティング システムの更新を試して最新のドライバーをインストールします。

### <a name="cuda"></a>CUDA

[CUDA](https://developer.nvidia.com/cuda-zone) は、NVIDIA によって考案された並列コンピューティング プラットフォームおよびプログラミング モデルです。 CUDA は、GPU のパワーを活用することで、計算のパフォーマンスを劇的に高めます。 現在、ディープ ラーニング フレームワークには CUDA Toolkit 8.0 が必要です。

CUDA をインストールするには

- こちらの[サイト](https://developer.nvidia.com/cuda-80-ga2-download-archive)にアクセスし、CUDA をダウンロードしてインストールします。
- CUDA ランタイム ライブラリがインストールされたことを確認し、%PATH% または $Path 環境変数に CUDA バイナリのパスを追加します。
- Windows での既定のこのパスは、"C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v8.0\bin" です。

![Windows に CUDA をインストールする](media/installation/install_cuda_win.png)

### <a name="cudnn"></a>cuDNN

[cuDNN](https://developer.nvidia.com/cudnn) (CUDA Deep Neural Network ライブラリ) は、NVIDIA によるディープ ニューラル ネットワーク用のプリミティブの GPU で高速化されたライブラリです。 最新のディープ ラーニング フレームワークでは、cuDNN v6 が必要です。

cuDNN をインストールするには:

- [NVIDIA Developer](https://developer.nvidia.com/rdp/cudnn-download) にアクセスし、最新のパッケージをダウンロードしてインストールします。
- cuDNN バイナリが格納されているディレクトリを、%PATH% または $Path 環境変数に追加します。
- Windows では、cudnn64_6.dll を "C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v8.0\bin" にコピーできます。

> [!NOTE]
> CNTK 2.0 や TensorFlow 1.2.1 などの古いディープ ラーニング フレームワークでは cuDNN v5.1 が必要です。 ただし、cuDNN の複数のバージョンを一緒にインストールできます。

### <a name="python"></a>Python

Python は、ディープ ラーニング アプリケーションの主要なプログラミング言語になっています。 **64 ビット**の Python ディストリビューションが必要であり、最善の互換性のためには [Python 3.5.4](https://www.python.org/downloads/release/python-354/) をお勧めします。

### <a name="to-install-python-on-windows"></a>Windows に Python をインストールするには

- 自分専用に Python ランチャーをインストールし、Python を %PATH% 環境変数に追加することをお勧めします。
- 必ず pip をインストールします。これは、Python で記述されたソフトウェア パッケージをインストールして管理するためのパッケージ管理システムです。

ディープ ラーニング フレームワーク自体のインストールに pip が必要です。

![Windows に Python をインストールする](media/installation/install_python_win.png)

Python 3.5 が正しくインストールされていることを確認し、端末で次のコマンドを実行して pip を最新バージョンにアップグレードする必要があります。

- **Windows**

  ```cmd
  C:\Users\test>python -V
  Python 3.5.4

  C:\Users\test>pip3.5 -V
  pip 9.0.1 from c:\users\test\appdata\local\programs\python\python35\lib\site-packages (python 3.5)

  C:\Users\test>python -m pip install -U pip
  ```

- **macOS**

  ```bash
  MyMac:~ test$ python3.5 -V
  Python 3.5.4

  MyMac:~ test$ pip3.5 -V
  pip 9.0.1 from /Library/Frameworks/Python.framework/Versions/3.5/lib/python3.5/site-packages (python 3.5)

  MyMac:~ test$ python3.5 -m pip install -U pip
  ```

### <a name="python-on-visual-studio"></a>Visual Studio での Python

Python は、拡張機能によって Visual Studio で完全にサポートされます。
詳細については、[Visual Studio 用の Python ツールのインストール](../python/installing-python-support-in-visual-studio.md)に関するページをご覧ください。

### <a name="numpy-and-scipy"></a>NumPy と SciPy

- **NumPy** は汎用的な配列処理パッケージであり、小規模の多次元配列の速度を損なうことなく任意のレコードの大きな多次元配列を効率的に操作するように設計されています。

- **SciPy** ("サイ パイ" と発音) は、NumPy に依存する数学、科学、エンジニアリング向けのオープン ソース ソフトウェアです。 バージョン 1.0.0 以降、SciPy は Windows の正式なビルド済みホイール パッケージになっています。

NumPy と SciPy をインストールするには、端末で次のコマンドを実行します。

```bash
pip3.5 install -U numpy scipy
```

> [!NOTE]
> 上のコマンドは、既存の古いまたは非公式のバージョン (例: Windows 用の http://www.lfd.uci.edu/~gohlke/pythonlibs/ のサードパーティ パッケージ) の NumPy と SciPy を最新の正式なバージョンにアップグレードします。

### <a name="microsoft-cognitive-toolkit-cntk"></a>Microsoft Cognitive Toolkit (CNTK)

[Microsoft Cognitive Toolkit](https://cntk.ai) は、有向グラフによって一連の計算ステップとしてニューラル ネットワークを記述する統合ディープ ラーニング ツールキットです。 CNTK は、プログラミング言語として Python と BrainScript の両方をサポートします。

> [!NOTE]
> 現在、CNTK は macOS をサポートしていません。

CNTK Python パッケージのインストールについては、[CNTK のインストール方法](/cognitive-toolkit/Setup-CNTK-on-your-machine)に関するページをご覧ください。

### <a name="tensorflow"></a>TensorFlow

[TensorFlow](https://www.tensorflow.org/) は、データ フロー グラフを使って数値計算を行うためのオープンソースのソフトウェア ライブラリです。 インストールについては、[こちら](https://www.tensorflow.org/install/)をご覧ください。

> [!NOTE]
> バージョン 1.2 の時点で、TensorFlow は macOS に対する GPU のサポートを提供しなくなっています。

### <a name="caffe2"></a>Caffe2

[Caffe2](https://caffe2.ai/) は、軽量でモジュール型のスケーラブルなディープ ラーニング フレームワークです。 オリジナルの Caffe を元にして作られている Caffe2 は、式、速度、モジュール性を考慮して設計されています。

現時点では、ビルド済みの Caffe2 Python ホイール パッケージはありません。

ソース コードからビルドする場合は、[こちら](https://caffe2.ai/docs/getting-started.html)をご覧ください。

### <a name="mxnet"></a>MXNet

[Apache MXNet (incubating)](https://mxnet.incubator.apache.org/) は、効率性と柔軟性の両方を想定して設計されたディープ ラーニング フレームワークです。 [シンボリック プログラミングと命令型プログラミング](http://mxnet.io/architecture/index.html#deep-learning-system-design-concepts)を**併用**して、効率性と生産性を最大にできます。

MXNet をインストールするには、端末で次のコマンドを実行します。

- GPU あり

  ```bash
  pip3.5 install mxnet-cu80==0.12.0
  ```

- GPU なし

  ```bash
  pip3.5 install mxnet==0.12.0
  ```

### <a name="keras"></a>Keras

[Keras](https://keras.io/) は Python で書かれたハイレベルのニューラル ネットワーク API であり、CNTK、TensorFlow、または Theano の上で実行できます。 高速の実験を可能にすることに重点を置いて開発されました。 優れた研究を行うために重要なのは、アイデアから結果まで可能な限り最小限の遅延で到達できることです。

Keras をインストールするには、端末で次のコマンドを実行します。

```bash
pip3.5 install Keras==2.0.9
```

### <a name="theano"></a>Theano

[Theano](http://deeplearning.net/software/theano/) は、多次元配列が含まれる数式を効率的に定義、最適化、評価できる Python ライブラリです。

Theano をインストールするには、端末で次のコマンドを実行します。

```bash
pip3.5 install Theano==0.9.0
```

### <a name="pytorch"></a>PyTorch

[PyTorch](https://pytorch.org/) は、2 つの高度な機能を提供する Python パッケージです。

- 強力な GPU の高速化を利用したテンソル計算 (NumPy と同様)
- テープ ベースの autograd (自動微分) システムを基に構築されたディープ ニューラル ネットワーク

PyTorch をインストールするには、端末で次のコマンドを実行します。

- **Windows**

  正式なホイール パッケージはまだありません。 [Anaconda](https://anaconda.org/pytorch/repo?type=all) または[カリフォルニア大学](https://www.lfd.uci.edu/~gohlke/pythonlibs/#pytorch)からサードパーティ製のパッケージをダウンロードできます。

  - 自分のホーム ディレクトリ (例: *C:\Users\test\pytorch*) に解凍します。
  - *C:\Users\test\pytorch\Lib\site-packages* を %PYTHONPATH% 環境変数に追加します。

    ```bash
    pip3 install http://download.pytorch.org/whl/cu80/torch-0.4.0-cp36-cp36m-win_amd64.whl
    pip3 install torchvision
    ```

- **macOS**

  ```bash
  pip3.5 install http://download.pytorch.org/whl/torch-0.2.0.post3-cp35-cp35m-macosx_10_7_x86_64.whl
  ```

  > [!NOTE]
  > macOS バイナリは CUDA をサポートしていません。CUDA が必要な場合はソースからインストールします。

- **Linux**

  ```bash
  pip3.5 install http://download.pytorch.org/whl/cu80/torch-0.2.0.post3-cp35-cp35m-manylinux1_x86_64.whl
  ```

  > [!NOTE]
  > この 1 つのパッケージで、GPU と CPU の両方がサポートされます。

最後に、Windows 以外には torchvision をインストールします。

```bash
pip3.5 install torchvision
```

### <a name="chainer"></a>Chainer

[Chainer](https://chainer.org/) は、柔軟性を目指した Python ベースのディープ ラーニング フレームワークです。 実行による定義アプローチ (動的計算グラフとも呼ばれます) に基づく自動微分 API と、ニューラル ネットワークを構築してトレーニングするためのオブジェクト指向の高度な API が提供されます。

CUDA のサポートを有効にするには、[CuPy](https://github.com/cupy/cupy) をインストールします。

```bash
pip3.5 install cupy
```

> [!NOTE]
> Windows で CUDA 8.0 を使用して CuPy をコンパイルするには、[Visual Studio](https://visualstudio.microsoft.com/) の 2015 バージョンまたは [Microsoft Visual C++ Build Tools](https://visualstudio.microsoft.com/visual-cpp-build-tools/) が必要です。

Chainer をインストールするには、端末で次のコマンドを実行します。

```bash
pip3.5 install chainer==3.0.0
```
