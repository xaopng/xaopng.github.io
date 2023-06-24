---
title: APSI安装及使用
abbrlink: 51463
date: 2023-06-24 21:40:06
tags:
---
{% blockquote APSI https://github.com/microsoft/APSI  %}
项目地址
{% endblockquote %}

{% blockquote Pam https://www.cnblogs.com/pam-sh/p/16009319.html  %}
参考教程文章
{% endblockquote %}

{% hideToggle Ubuntu20.04一键编译安装脚本 %}

在用户主目录`~`下新建脚本`build.sh`，填入下面内容，完成后修改文件权限`chmod 775 build.sh`  

```bash
#!/bin/bash

cd ~

sudo apt update -y
sudo apt install gcc g++ m4 openssl libgmp-dev libglib2.0-dev libssl-dev libsodium-dev libtool git wget lzip make -y 
sudo apt-get clean
echo "start compile cmake \n ------------------------------ \n" \
wget https://github.com/Kitware/CMake/releases/download/v3.21.3/cmake-3.21.3.tar.gz
tar xvf cmake-3.21.3.tar.gz
cd cmake-3.21.3/
./bootstrap --prefix=/usr/local/ 
sudo make && sudo make install 
cd .. 
sudo ln -s /usr/local/bin/cmake /usr/bin/cmake 
rm -rf cmake-3.21.3 cmake-3.21.3.tar.gz

function clone_repository() {
  local repository_url=$1
  local max_attempts=$2
  local attempt_num=0

  while [ $attempt_num -lt $max_attempts ]
  do
    git clone $repository_url && return 0
    attempt_num=$((attempt_num+1))
  done

  echo "Failed to clone repository after $max_attempts attempts"
  exit 1
}


apt-get update

apt-get install -y clang

apt-get install curl zip unzip tar pkg-config -y

clone_repository https://github.com/microsoft/vcpkg 3

./vcpkg/bootstrap-vcpkg.sh

#echo 'export PATH=${PATH}:/root/vcpkg' >> ~/.bashrc

#source ~/.bashrc

~/vcpkg/vcpkg install seal[no-throw-tran] kuku log4cplus cppzmq flatbuffers jsoncpp gtest tclap

clone_repository https://github.com/microsoft/APSI.git 3

# sed -i.bak 's/option(APSI_BUILD_TESTS ${APSI_BUILD_TESTS_OPTION_STR} OFF)/option(APSI_BUILD_TESTS ${APSI_BUILD_TESTS_OPTION_STR} ON)/g' ~/APSI/CMakeLists.txt

# sed -i.bak 's/cmake_dependent_option(APSI_BUILD_CLI ${APSI_BUILD_CLI_OPTION_STR} OFF "APSI_USE_ZMQ;APSI_USE_LOG4CPLUS" OFF)/cmake_dependent_option(APSI_BUILD_CLI ${APSI_BUILD_CLI_OPTION_STR} ON "APSI_USE_ZMQ;APSI_USE_LOG4CPLUS" ON)/g' ~/APSI/CMakeLists.txt

cd ~/APSI

mkdir build

cd build/

rm -f CMakeCache.txt

cmake -DCMAKE_TOOLCHAIN_FILE=~/vcpkg/scripts/buildsystems/vcpkg.cmake -DAPSI_BUILD_TESTS=ON -DAPSI_BUILD_CLI=ON ..

make
```

运行脚本

```bash
./build.sh
```

{% note   no-icon simple %}

运行中途可能会选择时区，依次输入`6`和`70`，表示选择`Asia`和`Shanghai` 

{% endnote %}

{% endhideToggle %}

{% hideToggle 测试脚本%}

在`~/APSI/build/bin/`目录下新建脚本`test.sh`，填入下面内容，完成后修改文件权限`chmod 775 run.sh`

```bash
#!/bin/bash
python3 ~/APSI/tools/scripts/test_data_creator.py 10000 100 10

./sender_cli -d ~/APSI/build/bin/db.csv -p ~/APSI/parameters/1M-256.json -c -t 1 > tmp1.out &

./receiver_cli -q ~/APSI/build/bin/query.csv -t 1 -o ~/APSI/build/bin/test_0_100_10_0_64.csv > tmp2.out

echo "=============sender============="
cat tmp1.out
echo "=============receiver============="
cat tmp2.out

pid=`ps -ef | grep sender_cli | grep -v grep | awk '{print $2}'`
if [ "$pid" != "" ]; then
        echo kill api
        kill -9 $pid
fi
```

运行脚本

```bash
./run.sh
```
{% endhideToggle %}
