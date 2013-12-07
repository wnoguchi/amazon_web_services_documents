# Roadworker

Route53を設定ファイルで管理するツール。

## 環境

* Mac OS X Mavericks, MBA

## インストール

### Gemfile

僕はGemfileを用意します。

```ruby
source "https://rubygems.org"

gem 'roadworker'
```

そして

```
$ bundle install --path ~/vendor/bundle

Fetching gem metadata from https://rubygems.org/.........
Fetching gem metadata from https://rubygems.org/..
Resolving dependencies...
Using json (1.8.1)
Using mini_portile (0.5.2)
Using nokogiri (1.6.0)
Using uuidtools (2.1.4)
Installing aws-sdk (1.29.1)
Using systemu (2.5.2)
Installing macaddr (1.6.1)
Installing net-dns (0.8.0)
Installing tins (0.13.1)
Installing term-ansicolor (1.2.2)
Installing uuid (2.3.7)
Installing roadworker (0.3.10)
Using bundler (1.3.5)
Your bundle is complete!
It was installed into /Users/noguchiwataru/vendor/bundle
```

特にhomebrewでインストールするパッケージが必要なわけでもなくインストールできた。

```
$ bundle exec roadwork --version
roadwork 0.3.10
```

## 使う

当然ですが、AWS APIアクセスのためのアクセスキーに関する環境変数が事前にセットアップされている必要があります。

```bash
export AWS_ACCESS_KEY_ID='...'
export AWS_SECRET_ACCESS_KEY='...'
```

### 初期設定

Routefileに現在管理されているhosted_zoneの設定を出力する。

```
$ bundle exec roadwork -e -o Routefile

Export Route53 to `Routefile
```

### 中身はどうなっているか

```ruby
hosted_zone "example.com." do
  rrset "example.com.", "A" do
    ttl 300
    resource_records(
      "11.33.99.91"
    )
  end

  rrset "*.example.com.", "A" do
    ttl 300
    resource_records(
      "11.33.99.91"
    )
  end

  rrset "yunocchi.example.com.", "CNAME" do
    ttl 300
    resource_records(
      "hatenablog.com"
    )
  end

  rrset "miyako.example.com.", "A" do
    ttl 300
    resource_records(
      "111.222.333.444"
    )
  end

  rrset "nori.example.com.", "CNAME" do
    ttl 300
    resource_records(
      "domains.tumblr.com"
    )
  end
end
```

### 適用してみる

* まずは `--dry-run` してみる。

```
$ bundle exec roadwork --dry-run -a -f Routefile

Apply `Routefile` to Route53 (dry-run)
Update ResourceRecordSet: example.com. A (dry-run)
  set resource_records=[{:value=>"11.33.99.91"}] (dry-run)
Update ResourceRecordSet: *.example.com. A (dry-run)
  set resource_records=[{:value=>"11.33.99.91"}] (dry-run)
No change
```

問題なければ適用。  
2回目の実行ではちゃんと変更なしとなっている。  
冪等性ばんざい。

```
$ bundle exec roadwork -a -f Routefile
Apply `Routefile` to Route53
Update ResourceRecordSet: pg1x.com. A
  set resource_records=[{:value=>"11.33.99.91"}]
Update ResourceRecordSet: *.pg1x.com. A
  set resource_records=[{:value=>"11.33.99.91"}]

$ bundle exec roadwork -a -f Routefile
Apply `Routefile` to Route53
No change
```

AWS Management Console上で見てみるとちゃんと適用できている。  
すばらしい。

### いじわるしてみる

AWS Management Console上でレコードを1行追加してみました。  
本来ならRoutefile上で管理するつもりなので、あってはならないことです。  
まあ、コンテキストによってはAWS Management Console上で変更したやつはRoutefileにも反映してほしい気もしますが、  
そんな虫のいい話はないですね。  
**なので、ここではRoutefileにないレコードは消えてくれることを期待します。**

```
$ bundle exec roadwork --dry-run -a -f Routefile

Apply `Routefile` to Route53 (dry-run)
Delete ResourceRecordSet: localns.pg1x.com. A (dry-run)
No change
```

余計な行が増えているよと教えてくれました。  
`--dry-run` を消して適用すればOKです。  
AWS Management Console上からはきれいさっぱり消えています。

## References

- [【AWS】Route53をgitで管理する「Roadworker」を早速試してみました ｜ Developers.IO](http://dev.classmethod.jp/cloud/aws/route53-as-code-roadworker/)
- [File: README — Documentation for roadworker (0.3.2)](http://rubydoc.info/gems/roadworker/0.3.2/file/README.md)
- [winebarrel / Roadworker — Bitbucket](https://bitbucket.org/winebarrel/roadworker)
