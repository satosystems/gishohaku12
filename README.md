# 生成 AI 時代の Python 環境構築指南

みなさん、生成 AI を活用していますか？

<img src="img/generative-ai.png" alt="Generative AI" width="800" />

生成 AI という概念は 2014 年に登場し、OpenAI によって 2019 年には GPT-2、2020 年には GPT-3（高校生レベル）、2023 年には GPT-4（大学生レベル）、2025 年に GPT-5（博士号レベル）と発展しています[^gpt-level]。その中でも 2022 年に登場した ChatGPT が、AI 利用をチャットという使いやすい対話 UI に落とし込んだことで、専門家しか使えなかった生成 AI を大衆の日常ツールへと押し上げ、以降の各社競争を一気に加速させることになりました。ChatGPT はインターネット登場に匹敵するインパクトであると見る専門家もいるほどです[^impact]。AI の学習に利用する GPU を提供する最大手 NVIDIA の株価は、2022 年比で 10 倍以上の値を付けています[^NVIDIA]。

メディア企業 Future の 2025 年 9 月のグローバル調査では、米国 55%、英国 62% が「従来の検索より生成 AI を使う」と回答しており[^tomsguide]、消費者層における生成 AI の浸透がますます進む兆しです。Google は 2024 年 8 月から検索結果に「AI による概要」を展開しており[^AI-overview]、2025 年 9 月には検索結果の「すべて」の更に左に「AI モード」というタブが追加されています[^AI-mode]。Yahoo! Japan は Google に先駆け 2025 年 4 月に「AI アシスタント」をリリースしており、検索の代わりに AI とチャットで知りたい内容を問い合わせることができるようになりました[^Yahoo]。Microsoft の Bing にも Copilot タブが提供されていますが、こちらは検索内容をクエリに持つ Copilot へのリンクなので、検索を置き換えるという UX にまでは至っていません。

The Browser Company は 2025 年 5 月に同社の人気ブラウザ Arc の積極的な開発を中止し、今後は AI ブラウザ Dia に注力すると発表しました[^arc]。Microsoft も Edge を Copilot ファーストへ舵を切っています[^edge]。また今後の Windows PC には Copilot キーが備わり、より AI が使いやすい環境が整備されます[^copilot-key]。Microsoft は Office 製品にも Copilot を組み込み[^office]、Google は Google Drive に Gemini を搭載し[^gemini-in-google-drive]、ますます日常的に AI が利用・浸透していく世の中になっています。Google の「OK Google」も一部の最上位モデルのスマートフォンでは Google アシスタントから Gemini に置き換わりつつあります。Android ユーザーは手元のスマートフォンで今すぐ Google アシスタントを Gemini に置き換えることができるかもしれません[^switch-to-gemini]。筆者もその利便性を実感しており、ぜひ試していただきたいです。

## Python 環境構築の必要性

このような AI ブームの中で、Python の利用がますます盛んになっています。Python は機械学習やデータサイエンスの分野で特に人気があり、これらの分野での研究や開発を行うためには Python 環境構築が不可欠です。

<img src="img/ai-vs-python.png" alt="AI v.s. Python" width="800" />

しかし、Python 環境の構築は初心者にとっては難しい場合があります。特に、複数のプロジェクトを同時に進める場合や、異なるバージョンの Python を使用する場合には、環境の管理が複雑になり、適切な管理ツールの選定が重要になります。

## ガイドの目的

このガイドの目的は、初心者でも簡単に Python 環境を構築できるようにすることです。具体的には、以下の点を重視しています。

- **簡単さ**: 複雑な手順を避け、できるだけシンプルな方法で環境を構築します。
- **柔軟性**: 複数のプロジェクトや異なるバージョンの Python を簡単に管理できるようにします。
- **実用性**: 実際の開発や研究に利用するプロジェクト管理ツールを紹介します。

このガイドを通じて、初心者の方々が Python 環境をスムーズに構築し、AI やデータサイエンスの分野での活動を始める手助けができれば幸いです。

## 対象読者

このガイドは、以下のような方々を対象としています。

- **初心者**: Python 環境の構築に不慣れな方。
- **学生**: 学校や大学で Python を学び始めた方。
- **開発者**: Python を使った開発を始めたい方。

## 免責事項

このガイドはあくまで筆者の調査と経験に基づくものであり、すべての環境や状況に適用できるわけではありません。特定のツールやライブラリの使用に関しては、公式ドキュメントを参照し、自己責任で行ってください。また、著者の普段使用している環境が macOS であるため、Windows や Linux 環境での手順は異なる場合があるため、適宜読み替えてください。実用的な内容を心がけていますが、読み物としても楽しめるように努めていますので、冗長な部分があるかもしれません。

## Python のバージョニング

macOS や多くの Linux のディストリビューションでは、Python がプリインストールされている場合があります。しかし、システムにプリインストールされている Python は、システムの管理や他のアプリケーションで使用されることがあるため、開発用には別途インストールすることを強くお勧めします。

<img src="img/pythons.png" alt="Python versioning" width="800" />

どのように Python をインストールするかは、その方の Python の利用目的や好みによります。以下にいくつかの方法を紹介します。

- python.org からのインストール（macOS/Linux/Windows）
- Homebrew/MacPorts を使ったインストール（macOS）
- Chocolatey/Scoop/WinGet を使ったインストール（Windows）
- Windows ストアを使ったインストール（Windows）
- venv/virtualenv を使ったインストール（macOS/Linux/Windows）
- pyenv を使ったインストール（macOS/Linux）
- Anaconda/Miniconda を使ったインストール（macOS/Linux/Windows）
- Windows Subsystem for Linux 2 (WSL2) を使ったインストール（Windows）
- Docker を使ったインストール（macOS/Linux/Windows）

筆者のおすすめは pyenv[^pyenv] です。pyenv は複数の Python バージョンを簡単に管理できるため、プロジェクトごとに異なるバージョンの Python を使用する場合に必須です。mise[^mise] や asdf[^asdf] も同様の機能を提供しますが、筆者は長年 anyenv[^anyenv] で様々な言語の *env 自体を管理しており、anyenv 経由で pyenv をインストールし利用しています。なお、筆者の手元の環境では、anyenv で goenv、jenv、nodenv、pyenv、rbenv を管理しています。

なお、Windows 環境では pyenv は利用できないため、WSL2 環境を構築して pyenv を利用することをおすすめします。WSL2 であれば Visual Studio Code の Remote-WSL を使って、Windows 上で Linux 環境の開発が可能です[^remote-wsl]。PyCharm も WSL2 環境をサポートしているので[^pycharm]、JetBrains 派の方もご安心ください。

## ライブラリ・プロジェクト管理ツールの戦国時代

<img src="img/warring-states-period.png" alt="img/Warring States Period" width="800" />

Python のライブラリやプロジェクトの管理には、後述のツールがよく使われます。ここではこれらの管理ツールが pyproject.toml を扱えるか、依存関係を pyproject.toml にコマンドで自動追記できるか、およびタスクランナー機能があるかどうかに焦点を当てます。

- pip
  - 公式 URL: <https://pip.pypa.io/>
  - pyproject.toml 対応: 部分的。pyproject.toml にある依存・ビルドシステム指定を使ってライブラリをインストールすることはできるが、`pip install <library>` で pyproject.toml に自動追記はしてくれず、一般的には requirements.txt を使用することが多い。また、pip はタスクランナーとしての機能は持たない。pip は Python 3.4 以降に標準で付属してくるため、ライブラリ管理ツールのデファクト・スタンダードとも言えるが、プロジェクト管理という観点では十分とは言えない。
- pipx
  - 公式 URL: <https://pipx.pypa.io/>
  - pyproject.toml 対応: 未対応。pipx はそもそもグローバルにインストールする CLI ツールを隔離してインストールするためのツールであり、プロジェクト管理ツールではない。また pipx はタスクランナーとしての機能も持たない。Python のツールやコマンドのインストーラだと思っていただいて問題ない。
- Poetry
  - 公式 URL: <https://python-poetry.org/>
  - pyproject.toml 対応: 対応。`poetry add <library>` または `poetry add -D <library>` で pyproject.toml に依存関係が自動追記される。Poetry はタスクランナーとして特化した機能は持たない（`[tool.poetry.scripts]` セクションは本来ライブラリ利用者向けだが、開発中にも利用できる）。
ドキュメントやエコシステムは成熟しているが PEP 標準への準拠が完全ではなく、例えば PEP 621 の `[project]` ネームスペースは使わず独自の `[tool.poetry]` を使う。
- Pipenv
  - 公式 URL: <https://pipenv.pypa.io/>
  - pyproject.toml 対応: 未対応。Pipenv は Pipfile/Pipfile.lock を使い、pyproject.toml には対応していない。ただし `pipenv install <library>` や `pipenv run <script>` 等を Pipfile を通じて利用することはできる。Pipenv はその名の通り pip と virtualenv を統合し、単一のツールでライブラリのインストールと仮想環境の構築を行うことができる。
- PDM
  - 公式 URL: <https://pdm-project.org/>
  - pyproject.toml 対応: 対応。`pdm add <library>` または `pdm add -G <env> <library>`/`pdm add -dG <env> <library>` で pyproject.toml に依存関係が自動追記される。また、`pdm run <script>` でスクリプトを実行可能。PDM は PEP 標準への準拠が進んでおり、pyproject.toml の PEP 517/518/621/735 等標準に準拠している。
- uv
  - 公式 URL: <https://uv.pypa.io/>
  - pyproject.toml 対応: 対応。`uv add <library>` または `uv add --dev <library>` で pyproject.toml に依存関係が自動追記される。uv は単一の Python コードを実行するための `uv run <python>` コマンドを提供するが、他のツールのようなタスクランナーとしての機能は持たない。uv は Rust 製で高速とされる。
- Hatch
  - 公式 URL: <https://hatch.pypa.io/>
  - pyproject.toml 対応: 部分的。Hatch はライブラリの依存関係を開発者が pyproject.toml に手動で記述する必要がある。Hatch は環境ごとにスクリプトを `[tool.hatch.envs.<ENV>.scripts]` に定義でき、`hatch run <ENV>:<script>` でスクリプトを実行可能。Hatch は前述の通り、複数の仮想環境を柔軟に設定・管理できる点が大きな特徴。

まとめると以下のようになります。

| ツール | 依存関係自動追記 | タスクランナー機能 |
|:--:|:--:|:--:|
| pip | ✗ | ✗ |
| pipx | ✗ | ✗ |
| Poetry | ○ | △ |
| Pipenv | ✗ | ✗ |
| PDM | ○ | ○ |
| uv | ○ | ✗ |
| Hatch | ✗ | ○ |

今回取り上げたツールの中で、条件を満たすのは PDM だけです。

PDM は PEP のモダンな標準に準拠しており、`pyproject.toml` を唯一の設定ファイルとしてプロジェクト管理できます。標準仕様に準拠しているため、必要に応じて他のツールと併用することも可能ですし、pyproject.toml を扱う独自のツールも作りやすいです。場合によってはプロジェクト管理ツールを乗り換えやすいというのもメリットになります。npm のように、インストールしたパッケージをシステム全体でキャッシュすることができ、ストレージの節約とインストールの高速化に貢献しています。PEP で定義はされていませんが、pdm.lock というロックファイルを生成し、依存関係を `pdm sync` で復元できます。必要に応じてプラグインシステムを使用してカスタムコマンドの追加や挙動の変更が行えます。

PDM は `pip install pdm` でインストールできますが、公式には `pipx install pdm` でグローバルにインストールすることが推奨されています。PDM は Python 3.7 以降をサポートしています。現時点で 3.7 未満の Python を新規に使う理由はないので、このバージョン制約は特に問題にならないでしょう。

## まとめ

Python 環境の構築は、初心者にとっては難しい場合がありますが、適切なツールを使用することで簡単に管理できます。pyenv と PDM の組み合わせは、柔軟で実用的な Python 環境を提供します。このガイドを参考にして、Python 環境を構築し、AI 新時代に乗り遅れないようにしましょう。

[^gpt-level]: <https://www.asahi.com/articles/AST871V8KT87UHBI00RM.html>
[^impact]: <https://wired.jp/article/plaintext-chatgpt-year-of-living-generatively/>
[^NVIDIA]: <https://www.google.com/finance/quote/NVDA:NASDAQ?sa=X&sqi=2&ved=2ahUKEwihxuu3xM2PAxX-1TQHHdzYFWIQ3ecFegQIOhAT&window=MAX>
[^tomsguide]: <https://www.tomsguide.com/ai/ai-search-is-exploding-6-tasks-people-are-now-giving-to-ai-instead-of-google>
[^AI-overview]: <https://blog.google/intl/ja-jp/products/explore-get-answers/ai-overviews/>
[^AI-mode]: <https://blog.google/intl/ja-jp/products/explore-get-answers/ai-mode-search/>
[^Yahoo]: <https://news.yahoo.co.jp/articles/77c99cae1fd1f9564446da6546962ef804eaf365>
[^arc]: <https://gigazine.net/news/20250608-letter-to-arc-members/>
[^edge]: <https://blogs.windows.com/msedgedev/2025/07/28/introducing-copilot-mode-in-edge-a-new-way-to-browse-the-web/>
[^copilot-key]: <https://news.microsoft.com/ja-jp/features/230105-introducing-a-new-copilot-key-to-kick-off-the-year-of-ai-powered-windows-pcs/>
[^office]: <https://www.microsoft.com/ja-jp/microsoft-copilot/organizations>
[^gemini-in-google-drive]: <https://support.google.com/drive/answer/14356148?hl=ja>
[^switch-to-gemini]: <https://support.google.com/gemini/community-guide/311313264/>
[^pyenv]: <https://github.com/pyenv/pyenv>
[^mise]: <https://github.com/jdx/mise>
[^asdf]: <https://asdf-vm.com/>
[^anyenv]: <https://github.com/anyenv/anyenv>
[^remote-wsl]: <https://learn.microsoft.com/ja-jp/windows/wsl/tutorials/wsl-vscode>
[^pycharm]: <https://pleiades.io/help/pycharm/using-wsl-as-a-remote-interpreter.html>
