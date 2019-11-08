# ScalaSandboxByDocker
Dockerを使ってjava(openjdk13)とScala(2.13.1)の遊び場を作ってみる

## 初回起動時のお願い

`docker-compose up` しただけでは scala はインストールされないため、
`docker-compose exec openjdk bash` してコンテナのシェルを起動した後、 `bash /shells/install_scalaenv.sh` を実行してください
