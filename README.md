## 機能

- 高: チャンネルリストアップ(自動更新)
- 高: 視聴(mplayer2)
- 高: 自動帯域チェック(チャンネルリスト更新時)
- 高: お気に入り
- 低: ソート
- 低: 非表示機能(配信者名・詳細からブラックリスト生成)
- 低: 録画(ダンプ)
- 低: 各YPの配信統計

## 対応YP

カスタムできるようにしたい

### デフォルト

- SP: http://bayonet.ddo.jp/sp/index.txt
- TP: http://temp.orz.hm/yp/index.txt
- EventYP: http://eventyp.xrea.jp/index.txt
- CaveTube: http://rss.cavelis.net/index.txt
- http://yp.kymt.me/index.txt
- http://yp.kymt.me/livetubeindex.txt

## 自動帯域チェック

### SP

http://bayonet.ddo.jp/sp/uptest/

POST: http://bayonet.ddo.jp:444/sp/uptest.cgi

404で「It's not necessary to test.」っとでたらチェック通ってる

```javascript
<script language="JavaScript">
<!--
function init(){
  var data = "riouwerflksdhfzxcvmncvzxksdjafwperyqweroiwerpwqead";
  var data1 = "";
  var data2 = "";
  var len1 = 1000/data.length;
  var len2 = 250;

  for(var i=0; i<len1; i++){
    data1 += data;
  }
  for(var i=0; i<len2; i++){
    data2 += data1;
  }
  document.uptest.file.value = data2;
}
// -->
</script>
```

## FormData

- file: 250kbくらいの大きさ

## プレイヤー

### mplayer2のおすすめ設定

~/.mplayer/config か --include引数で設定ファイルをロード

```txt
# default configuration that applies to every file
[default]

# use X11 for video output, use a framebuffer as fallback
vo=gl3.x11,xv,directfb

# use alsa for audio output, choose oss4 as fallback
ao=alsa,oss

# multithreaded decoding of H264/MPEG-1/2 (valid: 1-8)
lavdopts=threads=2

# prefer using six channels audio
channels = 6

# scale the subtitles to the 3% of the screen size
subfont-text-scale = 3

# never use font config
nofontconfig = 1

# set the window title using the media filename, when not set with --title.
use-filename-title=yes

# add black borders so the movies have the same aspect ratio of the monitor
# for wide screen monitors
vf-add=expand=::::1:16/9:16

# for non wide screen traditional monitors
#vf-add=expand=::::1:4/3:16

# disable screensaver
heartbeat-cmd="xscreensaver-command -deactivate &" # stop xscreensaver
stop-xscreensaver="yes" # stop gnome-screensaver

# correct pitch when speed is faster or slower than 1.0
af=scaletempo

# allow to seek in a file which is still downloading whilst watching it
idx=yes

# allow to increase the maximal volume
#softvol=1
#softvol-max=600

# skip displaying some frames to maintain A/V sync on slow systems
framedrop=yes

# more intense frame dropping (breaks decoding)
#hardframedrop=yes

# profile for up-mixing two channels audio to six channels
# use -profile 2chto6ch to activate
[2chto6ch]
af-add=pan=6:1:0:.4:0:.6:2:0:1:0:.4:.6:2

# profile to down-mixing six channels audio to two channels
# use -profile 6chto2ch to activate
[6chto2ch]
af-add=pan=2:0.7:0:0:0.7:0.5:0:0:0.5:0.6:0.6:0:0
```

## License

GPLv3

## memo

http://www23.atwiki.jp/pecapiracy/pages/14.html

index.txt

```txt
(1)<>(2)<>(3)<>(4)<>(5)<>(6)<>(7)<>(8)<>(9)<>(10)<>(11)<>(12)<>(13)<>(14)<>(15)<>(16)<>(17)<>(18)<>(19)

(1) 配信チャンネル名
(2) チャンネルID
(3) 配信者のIPアドレス:PeerCast使用ポート
(4) コンタクトURL
(5) ジャンル
(6) 詳細
(7) 視聴者数(隠蔽する設定にしている場合は -1 になる)
(8) リレー数(隠蔽する設定にしている場合は -1 になる)
(9) ビットレート(kbps)
(10) ファイル形式
(11)
(12)
(13)
(14)
(15) 配信チャンネル名がURLエンコードされたもの
(16) 配信時間 (*注2)
(17) ステータス(通常は"click")
(18) 配信者からのコメント (*注1)
(19)
```

(2)が「00000000000000000000000000000000」の時は帯域チェックなどがひつよう

視聴URL

```txt
http://<Host:Port>/pls/(2)?tip=(3)
```
