# Emscriptenの導入

色々調べたが、pythonのバージョンに制約があったり、その他諸々の環境を整えるのは時間がかかるので、dockerを使うことにした。

``` sh
$ docker pull trzeci/emscripten
```


## ビルド
### linux系の場合
```
docker run \
  --rm \
  -v $(pwd):/src \
  -u emscripten \
  trzeci/emscripten \
  sh -c "cd wasm && emconfigure cmake && make"
```

### Windows PowerShell場合（pwdの仕様でこうなる）
```
docker run `
  --rm `
  -v "/$((pwd).Drive.Name.ToLowerInvariant())/$((pwd).Path.Replace('\', '/').Substring(3)):/src" `
  -u emscripten `
  trzeci/emscripten `
  sh -c "cd wasm && emconfigure cmake && make"
```


## 実行
docker で emrun を使って実行したいところだが、docker の --network=host が Windows / MacOS では動作しない。そうなると、bridge接続になるのだが、trzeci/emscripten は localhost でポートを開いているため、外からの接続ができない。従って、VSCode の Live Server を使った方が手っ取り早い。
ただし、wasm 拡張子を application/octed-stream で返却するため、ブラウザでエラーになるけど動く。
ちなみに、このエラーはブラウザが出しているものではなく、emscriptenのデフォルトで生成するhtmlが出力しているもの。

