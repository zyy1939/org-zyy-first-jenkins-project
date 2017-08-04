
<image src="https://github.com/zyy1939/org-zyy-first-jenkins-project/blob/master/src/main/webapp/image/backtrack.jpg" width="640px" hight="480px" />

# ========项目简介===========

    本项目用于搭建Jenkins自动化部署专用
    
## 一、环境搭建：

    1. jdk8.x环境
    2. maven 3.x
    3. git 2.5x 
    
## 二、项目实战

## 三、部署开始

## 四、配置项：

    #!/bin/bash 
    #copy file and restart tomcat 

    export JAVA_HOME=/home/soft/jdk1.8.0_73
    export CATALINA_HOME=/home/soft/tomcat-8.0.33
    export CATALINA_BASE=/home/soft/tomcat-8.0.33
    export BUILD_ID=dontKillMe

    tomcat_path=/home/soft/tomcat-8.0.33
    project=jenkins-project-web
    war_name=jenkins-project-web.war 
    war_path=http://192.168.32.101/:8080/jenkins/job/org-zyy-first-jenkins-project/ws/targetserver_port=8081
    file_path=~/.jenkins/workspace/org-zyy-first-jenkins-project/target

    TOMCAT_PID=`/usr/sbin/lsof -i :8081|grep -v "PID" | awk '{print $2}'`
    if [ "$TOMCAT_PID" != "" ];
    then
       echo "tomcat is running PID:$TOMCAT_PID"
       echo "must stop tomcat "
       $tomcat_path/bin/shutdown.sh
    else
       echo "tomcat is not running"
    fi

    sleep 3s 

    echo "rm -rf ${tomcat_path}/webapps/ROOT/*"

    rm -rf ${tomcat_path}/webapps/ROOT/*

    cd $file_path

    cp ${war_name} ${tomcat_path}/webapps/ROOT/

    cd $tomcat_path/webapps/ROOT/

    unzip ${war_name}

    rm -rf ${war_name}

    sleep 5s 

    #$tomcat_path/bin/startup.sh

    cd $tomcat_path/bin/
    ./startup.sh

    echo "server restarted"

