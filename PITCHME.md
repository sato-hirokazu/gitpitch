### ApplyjapanのServerspec

---
- 発生した問題 |
- provisioningにないけど、installがされている・・。 |
- supervisord、Redisって、使ってるんだっけ？ |
- そもそも、どんな設定だったか知らない・・・。|
---

---
- Serverspecとは何？ |
- Rspecでサーバのテストを行うためのツール |
- describe package('nginx') do
  it { should be_installed }
end
---

---
Applyjapanの構成
- WEB3台・DB2台(master/slave)・batch1台
---

---
悩み1
- 複数のホストで、共通のテストを実行したい |
---

---
解決策
- 構成 |

```
tree -L 1 spec/

spec/
├── batch
├── common
├── db
├── spec_helper.rb
└── web

```
---

---
悩み2
- 全サーバの一覧ってどう管理する？(たぶん、devとかもいれたら、サーバ数30〜40くらいある気がする...) |
---

---
解決策
- ymlで管理するようにした |
- bundle exec rake serverspec -T |

```
rake serverspec                         # Run serverspec to all hosts
rake serverspec:aj-api-db01             # Run serverspec to aj-api-db01
rake serverspec:aj-api-web01            # Run serverspec to aj-api-web01
rake serverspec:aj-api-web02            # Run serverspec to aj-api-web02
rake serverspec:aj-api-web03            # Run serverspec to aj-api-web03
rake serverspec:aj-dev-api01            # Run serverspec to aj-dev-api01
rake serverspec:aj-dev-db01             # Run serverspec to aj-dev-db01
rake serverspec:aj-dev-web01            # Run serverspec to aj-dev-web01
rake serverspec:aj-shikoku-web08        # Run serverspec to aj-shikoku-web08
... (省略)

```
---

### おわり
