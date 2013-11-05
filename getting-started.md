# Getting Started

## AWS Command Line Interface

- [AWS Command Line Interface](http://aws.amazon.com/jp/cli/)

* 環境変数の設定

```bash
# ~/.bash_profile
export AWS_ACCESS_KEY_ID=AKIAIOSFODNN7EXAMPLE
export AWS_SECRET_ACCESS_KEY=wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
export AWS_DEFAULT_REGION=ap-northeast-1
```

* インストール

```
pip install awscli
```

* 設定

```
mkdir ~/.aws
cat <<EOF >~/.aws/config
[default]
aws_access_key_id = AKIAIOSFODNN7EXAMPLE
aws_secret_access_key = wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
; Asia Pacific (Tokyo) Region
region = ap-northeast-1
EOF
```

アクセスキーとシークレットアクセスキーについては https://console.aws.amazon.com/iam/home?#security_credential へGo。

* 入力補完を有効にする(Bash)

```
complete -C aws_completer aws
```

* 使ってみる

以下は現在稼働中のインスタンスの情報を取得するコマンド。

```
aws ec2 describe-instances
```
