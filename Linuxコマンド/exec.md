# Summary   
コマンドを実行して終了する   

## Example    
```   
exec $SHELL --Login
```   
環境変数$SHELLをログインシェルから起動させることをexecする(シェルを再起動する)   

## More Detail    
exec lsのコマンドを考える↓(引用http://x68000.q-e-d.net/~68user/unix/pickup?exec)

<execを使わない場合>
- システムコールfork(2)を呼び、子プロセスを生成する。
- 子プロセスはlsをexec(2)する。
- 親プロセスであるシェルは、lsの実行が完了するのを待つ(waitする)。

<execを使う場合>
シェルはfork(2)せず、いきなりlsコマンドをexec(2)する(シェルの内部コマンドexec(1)を実行すると、内部でシステムコールexec(2)が呼ばれるということ)。
シェルのプロセス情報はlsのプロセスと情報で上書きされる。なお、子プロセスは生成されないので、シェルとlsのプロセスIDは同じになる。
