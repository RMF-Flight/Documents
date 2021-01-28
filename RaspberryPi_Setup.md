# OSの書き込み
[ダウンロードサイト](https://www.raspberrypi.org/software/)から、OSに合わせてRaspberry Pi Imagerをダウンロードして、実行する。指示に従ってOSを書き込む。

> なお、64GB以上のマイクロSDカードを使う場合は、OSを書き込む前に、Eraseを使ってFAT32でフォーマットし直す必要があります。(OSの一覧の下の方にEraseがあります。)ラズパイがexFATでフォーマットされたマイクロSDカードからの起動に対応していないためです。

# SSHの準備（無線環境）
microSDのルートディレクトリに"ssh"という空ファイル（拡張子不要）を作る。同様に、ルートディレクトリに"wpa_supplicant.conf"というファイルを作り、こちらには以下を記述する。

```wpa_supplicant.conf
country=JP
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
network={
    ssid="[SSID]"
    psk="[パスワード]"
}
```

# SSH
ターミナルに`ssh pi@raspberrypi.local`を打ち込む。つながったらパスワードとして`raspberry`を入力してログインする。（画面上には打った文字は表示されない。）

## つながらない場合（Windows）
コマンドプロンプトで`arp -a`を入力する。（WSL上のUbuntuではうまくいかなかった。） **b8:27:e1** で始まるMACアドレスがあるはずなので、そのIPアドレスをメモする。IPアドレスが **192.168.1.8** だった場合は以下で接続する。

```
ssh pi@192.168.1.8
```
