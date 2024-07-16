# Base image olarak OpenJDK 8 kullanıyoruz 
# Docker image'ının temeli olarak OpenJDK 8 JDK'yı kullanır. Bu, Java uygulamalarını çalıştırmak ve geliştirmek için gerekli olan tüm araçları içerir.
FROM openjdk:8-jdk

# GlassFish sunucusunun 4.1.1 sürümünü indiriyoruz
ENV GLASSFISH_VERSION 4.1.1
ENV GLASSFISH_HOME /glassfish


# RUN wget: GlassFish 4.1.1 sürümünü belirtilen URL'den indirir.
# && unzip: İndirilen ZIP dosyasını / dizinine açar.
# && mv: Açılan dizini /glassfish4'ten /glassfish dizinine taşır.
# && rm: ZIP dosyasını siler, böylece gereksiz dosyalar image içinde yer kaplamaz.
RUN wget http://download.oracle.com/glassfish/4.1.1/release/glassfish-${GLASSFISH_VERSION}.zip \
    && unzip glassfish-${GLASSFISH_VERSION}.zip -d / \
    && mv /glassfish4 ${GLASSFISH_HOME} \
    && rm glassfish-${GLASSFISH_VERSION}.zip

# Proje dosyalarını container'a kopyalıyoruz
COPY . /usr/src/app

# Proje dizinine gidiyoruz
# Bu, sonraki komutların bu dizin içinde çalıştırılacağı anlamına gelir.
WORKDIR /usr/src/app

# WAR dosyasını manuel olarak oluşturuyoruz
# GlassFish, bu dizine kopyalanan WAR dosyalarını otomatik olarak dağıtır.
RUN jar cvf HelloWeb.war .

# Oluşturduğumuz WAR dosyasını GlassFish autodeploy dizinine kopyalıyoruz
RUN cp HelloWeb.war ${GLASSFISH_HOME}/glassfish/domains/domain1/autodeploy/

# GlassFish'in HTTP portunu açıyoruz
# 8080 portu HTTP trafiği için, 4848 portu ise GlassFish yönetim konsolu için kullanılır.
EXPOSE 8080 4848

# GlassFish sunucusunu başlatıyoruz
CMD ["sh", "-c", "${GLASSFISH_HOME}/bin/asadmin start-domain -v"]