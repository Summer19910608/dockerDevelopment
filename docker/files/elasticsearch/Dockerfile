#Docker image of elasticsearch with ik tokenizer
# VERSION 6.5.0
# Author: bolingcavalry

#基础镜像使用elasticsearch:6.5.0
FROM elasticsearch:6.5.0

#作者
MAINTAINER BolingCavalry <zq2599@gmail.com>

#es插件目录
ENV ES_PLUGINS_PATH /usr/share/elasticsearch/plugins

#定义maven的安装目录
ENV MAVEN_BASE_PATH /opt

#定义编译ik分词器源码的目录
ENV IK_SRC_COMPILE_PATH /opt/ik_build

#maven解压后的文件夹名称
ENV MAVEN_PACKAGE_NAME apache-maven-3.6.0

#将maven的bin目录加入PATH
ENV PATH="${MAVEN_BASE_PATH}/${MAVEN_PACKAGE_NAME}/bin:${PATH}"

#进入要安装maven的文件夹
RUN cd $MAVEN_BASE_PATH && \
#下载maven压缩包
wget https://mirrors.tuna.tsinghua.edu.cn/apache/maven/maven-3/3.6.0/binaries/apache-maven-3.6.0-bin.tar.gz && \
#解压maven
tar -zxvf ${MAVEN_PACKAGE_NAME}-bin.tar.gz && \
#创建编译ik分词器源码的目录
mkdir $IK_SRC_COMPILE_PATH && \
#进入编译ik分词器源码的目录
cd $IK_SRC_COMPILE_PATH && \
#下载ik源码包
wget https://codeload.github.com/medcl/elasticsearch-analysis-ik/zip/master && \
#解压源码包
unzip master && \
#进入解压后的目录
cd elasticsearch-analysis-ik-master && \
#通过maven构建
mvn clean package -U -DskipTests && \
#创建ik文件夹
mkdir $ES_PLUGINS_PATH/ik && \
#构建成功后，将文件移动到插件目录
mv target/releases/*.zip $ES_PLUGINS_PATH/ik && \
#cd到ik文件夹
cd $ES_PLUGINS_PATH/ik && \
#解压
unzip *.zip && \
#进入要安装maven的文件夹
cd $MAVEN_BASE_PATH && \
#删除不需要的文件夹
rm -rf ${MAVEN_PACKAGE_NAME}-bin.tar.gz ${MAVEN_PACKAGE_NAME} && \
#删除ik的源码目录
rm -rf $IK_SRC_COMPILE_PATH