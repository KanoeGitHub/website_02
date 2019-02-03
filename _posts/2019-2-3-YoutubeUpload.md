---
published: true
layout: post
title: PS4のキャプチャー(録画)動画をYoutubeに高画質でアップロードする方法(アップコンバートのメリット)
author: Kanoe
categories: 雑記
tags:
- Youtube

---

本日2月3日の午前4時に Fortnite のゲーム内で DJ Marshmello のライブイベントがありました。<br>
世界的大人気DJの Marshmello さんのライブがゲーム内で見れるって最高ですよね。<br>
このイベントの数日前にPS4からPS4 Proに乗り換えたので、かなり綺麗な映像でライブを楽しめました。<br>
また、せっかく1080pで動画をキャプチャーできるようになったのだから試しにYoutubeにライブのプレイ動画をあげてみようと思います。<br>
<!-- more -->
<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Round ✌🏻 let’s go!!! <a href="https://twitter.com/FortniteGame?ref_src=twsrc%5Etfw">@FortniteGame</a> <a href="https://t.co/vVcHCcNeNE">pic.twitter.com/vVcHCcNeNE</a></p>&mdash; marshmello (@marshmellomusic) <a href="https://twitter.com/marshmellomusic/status/1091814963918688256?ref_src=twsrc%5Etfw">February 2, 2019</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script> 
<br>
<br>

# 本題
さて、動画をアップロードします。<br>

ちょこっとだけFCPXを使って編集して、H.264で書き出してあげます。<br>
書き出したサイズはもちろん1080pで、良い感じに再生できる。<br>
これをYoutubeにそのままアップロードしてみました。が...<br><br>

#### <font color="Red" size="6"> 画質落ちてない??? </font>
<br>

それが以下の動画<br>
<iframe width="560" height="315" src="https://www.youtube.com/embed/MQ3oxc4yt4g" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<br>
確かに普通のPS4の720pよりは綺麗に写っていますが、実際アップロード前の1080pの動画より画質が落ちています。<br>
<br>
そこでなんとなく「4Kにしちゃえ！」ってことで、FCPXのプロジェクトの設定を1080pから4Kに変えてアップロードしてみました。<br>
それが以下の動画<br>
<iframe width="560" height="315" src="https://www.youtube.com/embed/jjx_u1-EzOc" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<br>
1080pで見ると前の動画と相変わらず、画質は悪いままですが一つ上の1440pでみて見ると明らかに画質が上がっていると思います。<br>
<br>
特に、ライブ中の特殊効果とかがわちゃわちゃしてるシーンだと顕著だと思います。<br>
<br>
多分ですが、Youtube側でエンコードする際のビットレートが原因じゃないかなと。<br>
<br>
公式のヘルプに記載があります。<br>
[https://support.google.com/youtube/answer/1722171?hl=ja](https://support.google.com/youtube/answer/1722171?hl=ja)
<br>
これによると、PS4のキャプチャー動画はProであるないに関わらず30FPSなので、1080pだと８Mbps、1440pだと16Mbpsということから、ビットレートが上がる分細かい表現がより描画されているのかなと思います。<br>
<br>
4Kだとなおさらだと思うのですが、4K対応モニター持っていないのでこちらは正直なところよくわかりません（笑）<br>
<br>
# まとめ
あとでこのことについてググって見ると、記事は少ないもののアップコンバートしたほうがいいという記事がちらほらありました。<br>
<br>
[https://kamaci.jp/blog-entry-137.html](https://kamaci.jp/blog-entry-137.html) とかはより実験的に書いています。<br>
<br>
要するに、1080pそのままアップすると、ビットレートをかなり低くされてしまうため画質を良くするためには可能な限り大きい解像度でアップロードすることが大事ということです。<br>
<br>
この記事にも書いている通り、近い将来4Kモニタが主流になることでしょうから特にこれからもYoutubeに動画をあげて残していきたいという方は4Kでアップしていってもいいかもしれません。<br>
<br>
# 後記
4Kの動画を編集するにはそこそこのスペックのPCが必要となります。また、今回の4K版の動画の長さで約6.5GBあったので書き出す際にはさらに空き容量が必要となります。ただ、画質は良くなるのでオススメです。<br>
また、今回は使用していませんが、FCPXには最近ノイズリダクションエフェクトが追加されましたので、アップコンバートする際に出てくるブロックノイズなどがノイズリダクションをかけることにより軽減されるかもしれません。<br>
ただでさえ、「お使いのPCでは4Kの編集はオススメしません」って忠告出てくるのにさらにエフェクト突っ込むと大変なことになりそうだったのでやめました。<br>
いいPC欲しいですね。<br><br><br>

<a href="https://geo.itunes.apple.com/jp/app/final-cut-pro/id424389933?mt=12&app=apps">Final Cut Pro - Apple</a><br>
<a href="https://geo.itunes.apple.com/jp/app/final-cut-pro/id424389933?mt=12&app=apps" style="display:inline-block;overflow:hidden;background:url(https://linkmaker.itunes.apple.com/ja-jp/badge-lrg.svg?releaseDate=2011-06-21T00:00:00Z&kind=desktopapp&bubble=macos_apps) no-repeat;width:165px;height:40px;"></a>

