---
title: Cloudflare
tags:
  - 2026/05
created: 2026-05-06
updated: 2026-05-07
draft: false
---
## トンネル

自宅サーバーに主に使う。仕組み的には、CloudflareがDNSをやってくれて、自宅サーバーを公開できるようになる。

![](/attachments/Pasted%20image%2020260506175713.png)

### 手順

1. cloudflareにおいて、使うドメインのDNSを登録する。
2. cloudflareのダッシュボードから ネットワーク > Tunnels 
3. トンネル作成 を選択
4. 案内に従って、環境設定やトンネル名を指定。
5. 同じ画面で接続ステータスが常に出るので、接続検出されたらOK。

![](/attachments/Pasted%20image%2020260506180248.png)

6. ネットワーク > Tunnels からつくった、トンネルを選択。
7. ルート から ルートを追加 を選択。
8. 公開アプリケーション を選択。
9. ポートを指定。

1パソコンで複数サイトの場合、トンネルは増やさずにルートを増やして、8,9をやる。

## 参考

1. [Cloudflare Tunnelを使う #cloudflare - Qiita](https://qiita.com/studio_haneya/items/17e48d0b03f673602fa5)
2. [Cloudflare Tunnel · Cloudflare Docs](https://developers.cloudflare.com/tunnel/)
