# Wannier.jl CLI 使い方

(2024/3/6　作成)

# 目的

Wannierizationを実行するためのJulia言語のパッケージの[https://github.com/qiaojunfeng/Wannier.jl](https://github.com/qiaojunfeng/Wannier.jl)(以下左のリンクのページを公式ページと呼ぶ)のcliの使い方のメモを載せる。cliはインストールしてしまえばJuliaの知識なしで使える。

Wannier.jlで使える重要な機能の一つが**Automated mixing of maximally localized Wannier functions into target manifolds** 

([https://www.nature.com/articles/s41524-023-01146-w](https://www.nature.com/articles/s41524-023-01146-w))である。

この方法は例えば価電子帯がbonding、伝導帯がanti-bondingの軌道からなるinitial guessの推定が難しいようなバンドの価電子帯(伝導帯)のみのバンドを抜き出したいときに有効である。

# 実行手順

1. Juliaをインストールする。(インストーラーとしては[https://github.com/JuliaLang/juliaup](https://github.com/JuliaLang/juliaup)などがある。)
2. [https://github.com/qiaojunfeng/Wannier.jl](https://github.com/qiaojunfeng/Wannier.jl)のページのReadme.mdのInstallationに従い、pkgでWannier.jlをインストールする。
3. CLIをインストールする。公式ページでは

```bash
julia --project deps/build.jl install 
```

でインストール可能と書いてあるが、このdepsはJuliaがインストールされたディレクトリの

/packages/Wannier/package_number下にある。

1. installされたcliコマンドを実行する。

(公式ページでは

```bash
~/.julia/bin/wannier
```

にinstallされると書いてあるが自分の環境ではwannierがwjlになっていた。)

## **Automated mixing of maximally localized Wannier functions into target manifoldsの実行方法**

**Automated mixing of maximally localized Wannier functions into target manifolds** 
の方法を利用するには

```bash
wannier splitvc <seed name of win/amn/mmn/eig>
```

を実行する。オプションなどは

```bash
wannier splitvc
```

を実行するとわかる。コマンドラインでバンド数などのオプションを入力するのは面倒なのでtomlファイルにバンド数などを入れ、

```bash
wannier splitvc --config <toml file>
```

を実行するとよいかも。

例として、8つのバンドを3グループに分けそれぞれのグループにWannierizationを行う場合の
インプットファイルの中身は

```toml
indices = [ [ 1, 2,], [ 3, 4, 5, 6,], [ 7, 8,], ]
outdirs = [ "val_1", "val_2", "cond_3",]
```
とする。
