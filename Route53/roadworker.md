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

```
$ bundle exec roadwork -e -o Routefile

Export Route53 to `Routefile
```

## References

- [【AWS】Route53をgitで管理する「Roadworker」を早速試してみました ｜ Developers.IO](http://dev.classmethod.jp/cloud/aws/route53-as-code-roadworker/)
- [winebarrel / Roadworker — Bitbucket](https://bitbucket.org/winebarrel/roadworker)
