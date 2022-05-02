# grpc go

[grpc-tutorial](https://github.com/ymmt2005/grpc-tutorial)

チュートリアルを少し変更して動作確認

詳細はWikiに書く予定...

## 実装方法
go 1.16

1. protobufをインストール
  ~~~zsh
  $ brew install protobuf
  $ protoc --version
  libprotoc 3.17.3
  ~~~

2. Go用のコンパイラをインストール

Go: protoc に protoc-gen-go, protoc-gen-go-grpc というプラグインを組み合わせてコンパイル
~~~zsh
$ go install google.golang.org/protobuf/cmd/protoc-gen-go@v1.26
$ go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@v1.1
~~~

pathを通しておく
~~~zsh
$ export PATH="$PATH:$(go env GOPATH)/bin"
~~~

3. proto/にperson.proto作成

4. pathを適宜書き換えて以下のコマンドを実行すると/protoにファイルが2つ自動生成される
~~~zsh
$ protoc -I. -Iinclude --go_out=module=github.com/maru0804/grpc-study:. proto/person.proto
$ protoc -I. -Iinclude --go-grpc_out=module=github.com/maru0804/grpc-study:. proto/person.proto
~~~

5. server/main.goを記述

動作確認
  ~~~zsh
  $ go run main.go
  2022/05/02 21:03:30 Waiting for gRPC request ....
  2022/05/02 21:03:30 --------------
  ~~~

5. client/main.goを記述

動作確認(別ターミナルで実行)

期待した出力であることを確認
  ~~~zsh
  $ go run main.go
  2022/05/02 21:16:48 Start Unary request
  2022/05/02 21:16:48 Response from Hello Server: message:"Hello,Thomas Lathan (30). email is Withown@example.net"
  ~~~
