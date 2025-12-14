# Description
Dexter Industries 製品群で共通して利用されるインストール用スクリプト集です。

# Installing

ローカルに clone 済みのスクリプトを使って `script_tools` をインストール／更新する最も基本的なコマンドは次のとおりです（`DexterInd` リポジトリ一式が `pi` ユーザーのホームディレクトリ `~/DexterInd` に clone 済みであることを前提とします）。

```bash
cd ~/DexterInd/RFR_Tools/scripts
bash install_tools.sh
```

このコマンドは、Pi 上にリポジトリを配置するだけで、パッケージや依存関係のインストールは行いません。

### Python Package Options

**Python パッケージのインストールを有効化する** には、`--install-python-package` オプションが必須です。これは `python` と `python3` の両方の実行ファイルに対して有効であり、`--use-python3-exe-too` 用かどうかを気にする必要はありません。

このコマンドに追加できる Python パッケージ関連のオプションは次の 3 つで、**相互に排他的** です。

* `--system-wide` - `sudo` を用いて、システム全体に Python パッケージをインストールします。

* `--user-local` - 指定ユーザーのホームディレクトリ内に Python パッケージをインストールします。特別な権限は不要です。

* `--env-local` - システム全体にインストールしますが、特別な権限を必要としません。このオプションを使うには virtualenv などの仮想環境が必要です。

ディストリビューションによっては、Python 3 を `python3` 実行ファイルでしか使用できない場合があります。その場合は `--use-python3-exe-too` オプションが必要です。

### Apt-Get Package Options

apt-get / deb パッケージ関連で追加できるオプションは次のとおりです。

* `update-aptget` - `sudo apt-get update` を実行します。
* `--install-deb-debs` - 一般的な依存パッケージをインストールするための `sudo apt-get install [dependencies]` を実行します。

### Selecting a Branch/Tag to Checkout

このインストールスクリプトには、利用したいブランチやタグ名を指定することもできます。ブランチ名は `master` / `develop` / `feature/*` / `hotfix/*` / `fix/` のような形式、タグ名は `v*` や `DexterOS*` のような形式を想定しています。  
**指定がない場合は `master` ブランチが使用されます。**

# Installation Examples

`sudo` を使って Python パッケージをインストールし、apt-get パッケージのインストールをスキップする例です（この場合、`--system-wide` はデフォルト有効のため省略可能です）。

```bash
cd ~/DexterInd/RFR_Tools/scripts
bash install_tools.sh --install-python-package --system-wide
```

Python パッケージだけをホームディレクトリ内にインストールし、apt-get パッケージをインストールしない例です。

```bash
cd ~/DexterInd/RFR_Tools/scripts
bash install_tools.sh --install-python-package --user-local
```

Python パッケージをホームディレクトリ内にインストールしつつ、`apt-get update` と apt-get 依存パッケージのインストールも行う例です。

```bash
cd ~/DexterInd/RFR_Tools/scripts
bash install_tools.sh --install-python-package --user-local --update-aptget --install-deb-deps
```

Python パッケージはインストールせず、指定したタグ `DexterOS2.0` が指すバージョンの `script_tools` だけを所定の場所に置く例です。

```bash
cd ~/DexterInd/RFR_Tools/scripts
bash install_tools.sh DexterOS2.0
```

`develop` ブランチのバージョンを利用したい場合は次のようにします。

```bash
cd ~/DexterInd/RFR_Tools/scripts
bash install_tools.sh develop
```

`python` と `python3` の両方の実行ファイル向けにパッケージをインストールしたい場合は次のようにします。

```bash
cd ~/DexterInd/RFR_Tools/scripts
bash install_tools.sh --install-python-package --use-python3-exe-too
```

# Updating

パッケージを更新する場合も、前述したのと同じ `install_tools.sh` コマンドを使います。
