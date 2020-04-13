# homestead_vagrant
homesteadを使ったlaravel環境です。

hogeproject/
hogeproject/data
hogeproject/project

というプロジェクトを作っておきます。
hogeproject配下で
```
$ git submodule add https://github.com/KatsutoshiOtogawa/homestead_vagrant.git
```

と実行することにより、
vagrant環境をsubmoduleとして
プロジェクトに追加します。
hogeproject/project
配下のプロジェクトが実際のプロジェクトになります。


dataディレクトリはプロジェクトのファイル以外でのGuestOS,HostOS間のファイル共有に
利用してください。
