###sprigcloud config server ��ͨ githup

1. �½� repository microservicecloud-config

2. ��ȡ ssh Э��� git ��ַ https://github.com/SamsaraCloud/microservicecloud-config.git

3.  �ڱ���Ŀ¼�½�git �ֿⲢ clone

   1. F:\git\microservicecloud-config  = F:\git\microservicecloud-config\microservicecloud-config
   2. git ���� git clone https://github.com/SamsaraCloud/microservicecloud-config.git

4. �ڱ���Ŀ¼ F:\git\microservicecloud-config �����½�һ�� application.yml (**���ļ�Ҫ�� utf-8 �ĸ�ʽ����**)

   ```yml
   spring: 
     profiles: 
       active: 
       - dev
   ---
   spring: 
     profiles: dev      #��������
     application: 
         name: microservicesloud-config-yangyun-dev
   ---
   spring: 
     profiles: test  # ���Ի���
     application: 
       name: microservicesloud-config-yangyun-test
   ```

5. ��yml �ϴ��� githup

   ![image/1568253786(1).jpg](image/1568253786(1).jpg)

6. �½� module microservicecloud-config-3344 Ϊ Cloud ��������ģ��

7. pom

   ```pom
   <dependencies>
           <!-- https://mvnrepository.com/artifact/org.springframework.cloud/spring-cloud-config-server -->
           <dependency>
               <groupId>org.springframework.cloud</groupId>
               <artifactId>spring-cloud-config-server</artifactId>
           </dependency>

           <!-- https://mvnrepository.com/artifact/org.eclipse.jgit/org.eclipse.jgit -->
           <!-- eclipse ����Config��Git�������org/eclipse/jgit/api/TransportConfigCallback -->
           <dependency>
               <groupId>org.springframework.cloud</groupId>
               <artifactId>spring-cloud-starter-config</artifactId>
           </dependency>

           <dependency>
               <groupId>org.springframework.boot</groupId>
               <artifactId>spring-boot-starter-jetty</artifactId>
           </dependency>
           <dependency>
               <groupId>org.springframework.boot</groupId>
               <artifactId>spring-boot-starter-web</artifactId>
           </dependency>
           <dependency>
               <groupId>org.springframework.boot</groupId>
               <artifactId>spring-boot-starter-test</artifactId>
           </dependency>
       </dependencies>
   ```

8. yml

9. �������� Config_3344_StartSpringCloudApp

10. windows �޸�hosts (C:\Windows\System32\drivers\etc\hosts)�ļ�����ӳ��, linux�� /etc/hosts�ļ�

  1. 127.0.0.1 config-3344.com

11. ����ͨ�� Config ΢�����Ƿ���Դ� githup �ϻ�ȡ��������

    1. ����΢���� 3344
    2. http://config-3344.com:3344/applicatoin-test.yml

12. ���ö�ȡ����

    1. host:port/{application}-{profile}.yml = http://config-3344.com:3344/applicatoin-test.yml

    2. host:port/{application}/{profile}/{label} = http://config-3344.com:3344/applicatoin/test/master 

    3. host:port/{label}/{application}-{profile}.yml = http://config-3344.com:3344/master/applicatoin-test.yml

       ?

### SpringCloud Config �ͻ�������

1. F:\git\microservicecloud-config\microservicecloud-config �´����ļ� microservicecloud-config-client.yml

   ```yml
   spring: 
     profiles: 
     active: 
     -dev
     
   ---
   server: 
     port: 8201
   spring: 
     profiles: dev
     application: 
       name: microservicecloud-config-client
   eureka: 
     client: 
       service-url: 
         defaultZone: http://eureka-dev.com:7001/eureka/

   ---
   server: 
     port: 8202
   spring: 
     profiles: test
     application: 
       name: microservicecloud-config-client
   eureka: 
     client: 
       service-url: 
         defaultZone: http://eureka-test.com:7001/eureka/
   ```

2. �ύ�ļ��� githup

3. �½� microservice-config-client-3355

4. pom

5. bootstrap.yml

   1. application.yml ���û��������Դ����

   2. bootstrap.yml ��ϵͳ�������Դ����, ���ȼ�����

   3. Spring Cloud �ᴴ��һ�� Bootstrap Context, ��Ϊ Spring Ӧ�õ� Application Context�� **��������**. ��ʼ����ʱ��, Bootstrap Context ������ⲿ��Դ�����������Բ���������, �����������Ĺ���һ�����ⲿ��ȡ�� Enviroment. Bootstrap �����и����ȼ�, Ĭ�������, ���ǲ��ᱻ�������ø���, Bootstrap Context �� Application Context ���Ų�ͬ��Լ��, ��������һ�� bootstrap.yml �ļ�, ��֤ Bootstrap Context �� Application Context ���õķ���

      ```yml
      # spring config client ��
      spring:
        cloud:
          config:
            name: microservicecloud-config-client  # �� git �϶�ȡ�� client ����Դ�ļ�, û�� .yml ��׺��
            profile: dev #  ���η��ʵ�������
            label: master     # git �ϴ����ڷ�֧, Ĭ�� master
            uri: http://config-3344.com:3344           # ��΢������������ȥ�� config server 3344 �ŷ���, ͨ�� SpringCloudConfig ��ȡ githup �ķ����ַ
        
      ```

6. application.yml

   ```yml
   spring:
     application:
       name: microservicecloud-config-client
   ```

7. �޸�hosts����ӳ��

   1. 127.0.0.1  client-config.com

8. �½� rest ��, ��֤�Ƿ��ܴ� githup �϶�ȡ����

   1. ConfigClientRest

9. �������� ConfigClient_3355_StartSpringCloudApp

10. ����

   1. http://client-config.com:8201/api/config

### SpringCloud Config ����ʵս

1. ��������

   1. F:\git\microservicecloud-config\microservicecloud-config ��
      1. �½��ļ� microservicecloud-config-eureka-config.yml
      2. �½��ļ� microservicecloud-config-dept-client.yml

2. �½� microservicecloud-config-eureka-client-7001

3. pom

   ```xml
       <dependencies>
           <dependency>
               <groupId>org.springframework.cloud</groupId>
               <artifactId>spring-cloud-starter-config</artifactId>
           </dependency>

           <dependency>
               <groupId>org.springframework.cloud</groupId>
               <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
           </dependency>
       </dependencies>
   ```

4. bootstrap.yml

   ```yml
   spring:
     cloud:
       config:
         name: microservicecloud-config-eureka-client # ��Ҫ��githup �Ϻ�������Դ����
         profile: dev
         label: master
         uri: http://config-3344.com:3344  # config server
   ```

5. application.yml

   ```yml
   spring:
     application:
       name: microservicecloud-config-eureka-client
   ```

6. ����

   1. ���� microservicecloud-config-3344 config ��������
   2. �������ð� eureka server microservicecloud-config-eureka-client-7001 

7.  ���ð� Config dept ΢�����ṩ��

   1. �¹��� microservicecloud-config-dept-client-8001
   2. bootstrap.yml
   3. application.yml

8. ��

9. ?

10.   

11.  

12.  

13.  

14.  

15.  

16. ?

    ?