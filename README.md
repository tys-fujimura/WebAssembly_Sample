# WebAssembly_Sample
## 動かし方
https://qiita.com/kuniatsu/items/c00ddf6214ff144f348f

基本的には上記サイトに従うが、サイト中のコードに「imporitObject」という変数を扱っている箇所がChrome上で動かなかった。
以下のように変更することで動作したので、そのように変更している。
```
  const config = {
      env: {
          abort:()=>{}
      }
  };
  WebAssembly.instantiateStreaming(fetch("/test.wasm"), config)
 .then(wasm=>{
    console.log(wasm)
    const ex = wasm.instance.exports;
    const exported_func = ex.export_func;
    const num = exported_func();
    document.querySelector("#test").innerHTML=num;
 })
```
  
コンパイルして出来上がったwasmファイルとhtmlファイルを静的サイトとしてホスティングしてアクセスすると「33」って表記が出てくる。
その「33」がWebAssemblyで定義したメソッドから返却された値。
