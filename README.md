# 読書ボット

## 概要

このプロジェクトは、Baidu の音声認識（ASR）および音声合成（TTS）API に接続するための Python クラス `AipSpeech` を実装しています。音声データをテキストに変換したり、テキストを音声データに変換したりする機能を提供します。

## 機能の概要

- **音声認識 (ASR)**: 音声データを入力し、テキストに変換します。
- **音声合成 (TTS)**: テキストを入力し、それを音声データに変換します。

## クラス構造

`AipSpeech` クラスは、`AipBase` クラスを継承しており、API リクエストとレスポンスを処理するためのメソッドを提供しています。

### 主なメソッド

- **_isPermission**:
  - 認証オブジェクトを受け取り、API アクセスの権限があるかどうかをチェックします（常に `True` を返します）。

- **_proccessRequest**:
  - API リクエストを処理するメソッドです。リクエストのパラメータやデータを正しい形式に変換し、アクセス権限を確認します。音声認識と音声合成で異なる処理を行います。

- **_proccessResult**:
  - API レスポンスを処理するメソッドで、データの整形やエラー処理を行います。エラーが発生した場合、元のレスポンス内容を含むエラーオブジェクトを返します。

- **asr (音声認識)**:
  - 音声データを PCM 形式で受け取り、Baidu の音声認識 API に送信します。結果として、音声をテキストに変換します。
  
  **入力パラメータ**:
  - `speech`: 音声データ
  - `format`: 音声ファイルのフォーマット（デフォルトは `pcm`）
  - `rate`: サンプリングレート（デフォルトは `16000`）
  - `options`: 追加のオプション

- **synthesis (音声合成)**:
  - テキストを音声に変換します。Baidu の API を使用して、テキストを音声ファイルに変換し、そのファイルを返します。
  
  **入力パラメータ**:
  - `text`: テキスト
  - `lang`: 言語（デフォルトは `zh`、中国語）
  - `ctp`: 音声形式のタイプ（デフォルトは `1`）
  - `options`: 追加のオプション

## 依存関係のインストール

ターミナルで以下のコマンドを実行して、必要なライブラリをインストールします：

```bash
pip install requests
使用方法
このクラスをインポートし、Baidu の API キーを設定した後、音声認識や音声合成を行うことができます。

python
复制代码
from aip import AipSpeech

# Baidu API の認証情報を設定
APPID = 'YOUR_APPID'
APPKEY = 'YOUR_APPKEY'
APPSECRET = 'YOUR_APPSECRET'

client = AipSpeech(APPID, APPKEY, APPSECRET)

# 音声認識の例
result = client.asr(speech, format='pcm')
print(result)

# 音声合成の例
result = client.synthesis('こんにちは、世界！', lang='zh')
print(result)
