# CentOS8にOpenJDKとScalaを入れるDockerfile

# imageはcentos:8
FROM centos:8

# インストールするscalaのバージョンを指定
ENV scala_version="2.13.1"

# ビルドに必要なCentOSのパッケージをインストール
# インストールするopenJDKは13
RUN yum -y update
RUN yum -y install wget git
RUN wget https://download.java.net/java/GA/jdk13/5b8a42f3905b406298b72d750b6919f6/33/GPL/openjdk-13_linux-x64_bin.tar.gz
RUN tar zxvf openjdk-13_linux-x64_bin.tar.gz
RUN mv jdk-13 /opt
RUN rm openjdk-13_linux-x64_bin.tar.gz
RUN touch /etc/profile.d/jdk13.sh
RUN echo "export JAVA_HOME=/opt/jdk-13" >> /etc/profile.d/jdk13.sh
RUN echo "export PATH=\$PATH:\$JAVA_HOME/bin" >> /etc/profile.d/jdk13.sh
# ホームディレクトリ以外の場所にscalaenvを入れようとしたが、ホームディレクトリ依存の処理があるためそのままにした
RUN git clone git://github.com/mazgi/scalaenv.git ~/.scalaenv
RUN touch /etc/profile.d/scalaenv.sh
RUN echo 'export PATH="~/.scalaenv/bin:${PATH}"' >> /etc/profile.d/scalaenv.sh
RUN echo 'eval "$(scalaenv init -)"' >> /etc/profile.d/scalaenv.sh
RUN curl https://bintray.com/sbt/rpm/rpm | tee /etc/yum.repos.d/bintray-sbt-rpm.repo
RUN yum -y install sbt
# MySQL関係に必要
# DBのバージョンはMySQL8なのでおまじないをかける
RUN rpm -ivh https://dev.mysql.com/get/mysql80-community-release-el7-2.noarch.rpm
# webコンテナからdbコンテナのDBを確認できるようにコマンドラインツールもインストール
RUN yum -y install mysql mysql-devel
