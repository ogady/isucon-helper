# 01 よく使うコマンド

## systemd関連

### [はじめてのsystemdサービス管理ガイド(Classmethod)](https://dev.classmethod.jp/articles/service-control-use-systemd/)

```sh
# 有効化されているUnitの一覧表示
$systemctl list-units

# Unitの有効化/無効化
$sudo systemctl enable ${Unit名}
$sudo systemctl disable ${Unit名}

# Unitの停止/起動/再起動
$sudo systemctl stop ${Unit名}
$sudo systemctl start ${Unit名}
$sudo systemctl restart ${Unit名}

# Unitの起動状態確認
$sudo systemctl status ${Unit名}
```

## logファイル監視

```sh
$less -qR
# Shift + f で "tail -f" と同様の動きになる
```

## ファイルを空にする（logファイル初期化するときとか）

```sh
$cp /dev/null hoge.txt
```
