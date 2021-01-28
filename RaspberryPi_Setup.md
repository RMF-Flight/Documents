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
ターミナルに `ssh pi@raspberrypi.local` を打ち込む。つながったらパスワードとして `raspberry` を入力してログインする。（画面上には打った文字は表示されない。）

## つながらない場合（Windows）
コマンドプロンプトで `ipconfig` を実行し、Wireless LAN adapter Wi-Fi欄のIPアドレスとサブネットマスクからラズパイのIPアドレスの見当をつける。（WSL上のUbuntuではうまくいかなかった。）あたりをつけたIPアドレスに応じて以下のコマンドのIPアドレスの部分を変えてコマンドプロンプトで実行する。

```
for /l %i in (0,1,255) do ping -w 1 -n 1 192.168.0.%i
```

もう一度 `ssh pi@raspberrypi.local` を打ち込んでみて、つながったらOK。それでも駄目だったら、コマンドプロンプトで `arp -a` を入力する。 **b8:27:e1** で始まるMACアドレス（ラズパイ4だと **DC:A6:32** ）があるはずなので、そのIPアドレスをメモする。例えば、IPアドレスが **192.168.1.8** だった場合は以下で接続する。

```
ssh pi@192.168.1.8
```

# パッケージの更新
パッケージの更新のために、以下のコマンドを順に実行する。
```
sudo apt update
sudo apt upgrade
```

# 各種インターフェースの有効化
再起動した後はSSHが切れるので、もう一度SSHをつなげる。
## カメラ
`sudo raspi-config` を入力する。

**3 Interface Options > P1 Camera** と進めていき、 **Would you like the camera interface to be enabled?** に対して、 **Yes** を選択する。 **Finish** を選び、 **Would you like to reboot now?** に対して、 **Yes** を選択し、再起動する。

`vcgencmd get_camera` を入力して、 `supported=1 detected=1` と出力されれば、カメラが認識されている。

## I2C
`sudo raspi-config` を入力する。

**3 Interface Options > P5 I2C** と進めていき、 **Would you like the ARM I2C interface to be enabled?** に対して、 **Yes** を選択する。 **Finish** を選び、 **Would you like to reboot now?** に対して、 **Yes** を選択し、再起動する。

適当なデバイスをI2Cで接続し、 `i2cdetect -y 1` を入力する。以下のような数字（アドレス）が表示されていればOK。（接続したものによって数字と数字の場所は違う。）
```
     0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f
00:          -- -- -- -- -- -- -- -- -- -- -- -- --
10: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
20: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
30: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
40: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
50: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
60: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
70: -- -- -- -- -- -- 76 --
```

## Serial Port
`sudo raspi-config` を入力する。

**3 Interface Options > P6 Serial Port** と進めていき、 **Would you like a login shell to be sccessible over serial?** に対して、 **No** を選択、 **Would you like the serial port hardware to be enabled?** に対して、 **Yes** を選択する。 **Finish** を選び、 **Would you like to reboot now?** に対して、**Yes** を選択し、再起動する。

"\boot\config.txt" ファイルの末尾に **dtoverlay=pi3-disable-bt** を追記・保存（ `sudo vi \boot\config.txt` などで編集）して再起動（ `sudo reboot` ）する。

RaspberryPiのGPIOの8番ピン（TX）と10番ピン（RX）を直接つなぎ、以下のファイルを作成・実行して `serial0 is working` と出力されればOK。（test.pyという名前で保存したら、 `python3 test.py` で実行）
```python
import serial
ser = serial.Serial('/dev/serial0', 115200, timeout=1)
test_string = 'test 1 2 3\n'.encode()
ser.write(test_string)
print('serial0 is working' if ser.readline() == test_string else 'error')
```