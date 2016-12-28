### mysql数据导入，索引更新，索引增量导入

1、数据库导入数据

1.1 创建core 目录#mkdir solrhome/db-core -p复制默认配置文件#cp solr-5.5.3/example/example-DIH/solr/db/* ./solrhome/db-core/ -r修改配置文件solrconfig.xml (solr-5.5.3目录下的contrib、lib 目录已被提制到solrhome 目录)：
```
<lib dir="${solr.install.dir:..}/dist/" regex="solr-dataimporthandler-.*\.jar" />

<lib dir="${solr.install.dir:..}/contrib/extraction/lib" regex=".*\.jar" />

<lib dir="${solr.install.dir:..}/dist/" regex="solr-cell-\d.*\.jar" />

<lib dir="${solr.install.dir:..}/contrib/langid/lib/" regex=".*\.jar" />

<lib dir="${solr.install.dir:..}/dist/" regex="solr-langid-\d.*\.jar" />

<lib dir="${solr.install.dir:..}/contrib/velocity/lib" regex=".*\.jar" />

<lib dir="${solr.install.dir:..}/dist/" regex="solr-velocity-\d.*\.jar" />

<!-- DIH 依赖jar -->

<lib dir="${solr.install.dir:.}/lib/" regex="solr-velocity-\d.*\.jar" />
```

1.2 在solrconfig.xml 中有如下配置，db-data-config.xml 是同solrconfig.xml 的相对路径，也可以使用绝对路径

```
<requestHandler name="/dataimport" class="solr.DataImportHandler">

<lst name="defaults">

<str name="config">db-data-config.xml</str>

</lst>

</requestHandler>
```

1.3 修改db-data-config.xml

```
<dataConfig>

<dataSource type="JdbcDataSource" driver="com.mysql.jdbc.Driver" url="jdbc:mysql://10.37.149.15:8066/BUSIDB" user="test_busi" password="test_busi"/>

<document>

<entity name="shop" query="SELECT main_user_id,shop_id id,shop_name FROM shop_info">

<field column="shop_name" name="shop_name" />

<field column="main_user_id" name="main_user_id" />

<field column="id" name="id" /><!-- 必须要有主键 -->

</entity>

</document>

</dataConfig>
```

1.4 上面配置的field 要在schema.xml文件中对应。在schema.xml 中配置如下，其中shop_name 使用mmseg4j中文分词
```
<!-- myself field -->

<field name="shop_name" type="textMaxWord" indexed="true" stored="true"/>

<field name="main_user_id" type="long" indexed="true" stored="true"/>

```
1.5 上传mysql 驱动到db-core/lib 目录下（在sorlconfig.xml中已经加载此目录的jar）。
1.6 导入数据库数据

1.7 搜索测试(左边查询框中，可以加入“排序”，分页等条件。)：

1.8 Java搜索代码

maven 依赖
```
<properties>

<solr.version>4.7.2</solr.version>

<slf4j_version>1.6.6</slf4j_version>

<log4j_version>1.2.16</log4j_version>

<jcl_version>1.1</jcl_version>

</properties>

<dependencies>

<!-- solr -->

<dependency>

<groupId>org.apache.solr</groupId>

<artifactId>solr-solrj</artifactId>

<version>${solr.version}</version>

<exclusions><!-- 去除依赖重复 -->

<exclusion>

<groupId>org.eclipse.jetty.orbit</groupId>

<artifactId>javax.servlet</artifactId>

</exclusion>

</exclusions>

</dependency>

<dependency>

<groupId>org.apache.solr</groupId>

<artifactId>solr-core</artifactId>

<version>${solr.version}</version>

<exclusions>

<exclusion>

<groupId>jdk.tools</groupId>

<artifactId>jdk.tools</artifactId>

</exclusion>

<exclusion>

<groupId>org.restlet.jee</groupId>

<artifactId>org.restlet</artifactId>

</exclusion>

<exclusion>

<groupId>org.restlet.jee</groupId>

<artifactId>org.restlet.ext.servlet</artifactId>

</exclusion>

<exclusion>

<groupId>org.eclipse.jetty.orbit</groupId>

<artifactId>javax.servlet</artifactId>

</exclusion>

</exclusions>

</dependency>

<!-- log -->

<dependency>

<groupId>log4j</groupId>

<artifactId>log4j</artifactId>

<version>${log4j_version}</version>

</dependency>

<dependency>

<groupId>org.slf4j</groupId>

<artifactId>slf4j-api</artifactId>

<version>${slf4j_version}</version>

</dependency>

<dependency>

<groupId>org.slf4j</groupId>

<artifactId>slf4j-log4j12</artifactId>

<version>${slf4j_version}</version>

</dependency>

<dependency>

<groupId>commons-logging</groupId>

<artifactId>commons-logging-api</artifactId>

<version>${jcl_version}</version>

</dependency>

</dependencies>

```

搜索：
```
public static void main(String[] args) throws Exception{

//solr 地址，db-core 是core 对应的名称

 HttpSolrServer solrServer = new HttpSolrServer("http://192.168.41.131:8080/solr/db-core");

 solrServer.setConnectionTimeout(20000);

 SolrQuery query = new SolrQuery();

 query.setParam("q", "shop_name:雾霾");

 QueryResponse rsp = solrServer.query(query);

 solrServer.optimize();

// 获取结果集

 SolrDocumentList docs = rsp.getResults();

 Long count = docs.getNumFound();//搜索结果数量

 Iterator<SolrDocument> iter = docs.iterator();

while (iter.hasNext()) {

 SolrDocument doc = iter.next();//SolrDocument 返回搜索数据的map

if (doc.getFieldValueMap() != null && doc.getFieldValueMap().size() > 0) {

 System.out.println(doc.getFieldValueMap());

 }

 }

}

```

2、索引添加，更新，删除2.1 添加文档索引，如果uniqueKey相同，solr自动会覆盖。2.2 根据uniqueKey 删除索引solr 控制台，更新索引：上面java代码搜索的结果为：{main_user_id=21200, id=10313, shop_name=雾霾天, _version_=1551891114117562368}使用solr控制台更新索引：


搜索结果：{main_user_id=21200, id=10313, shop_name=雾霾的天空, _version_=1551893320346632192}

shop_name 已经改变，同时version 也增加了。

索引的增加，删除，更新java代码如下（maven依赖同上）：

```
package com.convicteva.solr;

import org.apache.solr.client.solrj.SolrQuery;

import org.apache.solr.client.solrj.impl.HttpSolrServer;

import org.apache.solr.client.solrj.response.QueryResponse;

import org.apache.solr.common.SolrDocument;

import org.apache.solr.common.SolrDocumentList;

import org.apache.solr.common.SolrInputDocument;

import java.util.Iterator;

public class SolrTest {

public static void main(String[] args) throws Exception{

//solr 地址，db-core 是core 对应的名称

 HttpSolrServer solrServer = new HttpSolrServer("http://192.168.41.131:8080/solr/db-core");

 SolrTest solrTest = new SolrTest();

//添加文档

 solrTest.add(solrServer);

 solrTest.search(solrServer, "测试");

//更新文档

 solrTest.update(solrServer);

 solrTest.search(solrServer, "测试");

//删除文档

 solrTest.search(solrServer,"测试");

 solrTest.delete(solrServer);

 System.out.println("删除之后.....");

 solrTest.search(solrServer,"测试");

 }

private void add(HttpSolrServer solrServer) throws Exception{

 SolrInputDocument doc = new SolrInputDocument();

 doc.addField("main_user_id","12");

 doc.addField("id","1200");

 doc.addField("shop_name","这个是测试店铺名称");

 solrServer.add(doc);

 solrServer.commit();

 }

private void delete(HttpSolrServer solrServer) throws Exception{

//根据id 删除

 solrServer.deleteById("1200");

 solrServer.commit();

 }

private void update(HttpSolrServer solrServer) throws Exception{

//更新文档索引，如果id 存在则更新文档

 SolrInputDocument doc = new SolrInputDocument();

 doc.addField("main_user_id","12");

 doc.addField("id","1200");

 doc.addField("shop_name","这个是测试店铺名称2");

 solrServer.add(doc);

 solrServer.commit();

 }

private void search(HttpSolrServer solrServer,String keyWord) throws Exception{

 solrServer.setConnectionTimeout(20000);

 SolrQuery query = new SolrQuery();

 query.setParam("q", "shop_name:"+keyWord);

 QueryResponse rsp = solrServer.query(query);

 solrServer.optimize();

// 获取结果集

 SolrDocumentList docs = rsp.getResults();

 Long count = docs.getNumFound();//搜索结果数量

 Iterator<SolrDocument> iter = docs.iterator();

while (iter.hasNext()) {

 SolrDocument doc = iter.next();//SolrDocument 返回搜索数据的map

if (doc.getFieldValueMap() != null && doc.getFieldValueMap().size() > 0) {

 System.out.println(doc.getFieldValueMap());

 }

 }

 }

}

```


