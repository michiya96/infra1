## インフラ構築メモ１
#### WSL上でUbuntuを起動させる際に直面したエラー
#### Apache2などのシステムを起動させる際に以下のコマンドを実行するとこのようなエラーが発生した
##### $ systemctl status apache2
##### System has not been booted with systemd as init system (PID 1). Can't operate.Failed to connect to bus: Host is down

#### $ ps aux でプロセスの状態を確認すると以下のような結果になった
#####   USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
##### root         1  0.0  0.0    892   552 ?        Sl   15:30   0:00 /init
#### このことからPID１が上手く動作していないらしい
#### 動作させるには以下のURLに記載されているgenie -sコマンドを実行させる必要があるらしい
#### https://github.com/arkane-systems/genie
#### genie ｰsコマンドを実行すると少し時間がかかるが処理完了後先ほどの$ ps auxで確認すると
#####    USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
##### root           1  0.0  0.1 174704 11904 ?        Ss   20:01   0:03 systemd
#### 先ほどとは違いsystemdと表記され問題が解決出来たことが分かる
##### $ systemctl status apache2を実行するとApacheのステータスが確認出来るようになった
## 以上がインフラ構築初心者の一番の壁でした！！
