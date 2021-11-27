# 文档数据部分
### Document.java
- getTime()

查询三种索引下（默认，人工方法，智能方法）同一组负载下查询的时间；

返回值：long[]，不同索引下查询时间的数组；

抛出异常类型：UnknownHostException, ParseException；

<br/>

- getSingleQuery(String sql, int select)

分析单模态sql语句，完成查询；

输入值：查询语句sql；不同索引的选择（0为建立默认索引，1为建立人工推荐索引，2为建立只能推荐索引）

返回值：List<String>，查询结果ID的列表

抛出异常类型：UnknownHostException, ParseException；

<br/>

- getMultiQuery(String sql, int select)

分析多模态sql语句，完成查询；

输入值：查询语句sql；不同索引的选择（0为建立默认索引，1为建立人工推荐索引，2为建立只能推荐索引）

返回值：List<String>，查询结果ID的列表

抛出异常类型：UnknownHostException, ParseException；

### DocumentNew.java
接口函数与Document.java相同，修改了内部实现代码。

### JsonHandle.java
- jsonFormatter(String uglyJSONString)

将复杂的嵌套json字符串转换为路径json字符串，方便sql查询使用；

输入值：原始的嵌套json字符串

返回值：解除嵌套的路径json字符串

### QtFunc.java

- uploadData(String path)

将指定路径下的文档数据文件存入数据库

输入值：文档数据json文件的路径

返回值：当前文档数据相关信息的字符串列表（文档数据的细节与文档数据的结构）

返回值实例：

Details:

path:/Users/eclipse-workspace/mult/workload/workload_dox

This is a workload.

It contains 20010 nodes.

The frequent field:

document.date

Configurations:

name: workload1

eg:

Select document.id from document where document.date = 20120223;

Select document.id from document where document.date = 20100522;

Select document.id from document where document.date = 20100615;

Select document.id from document where document.date = 20091117;

Select document.id from document where document.date = 20100121;

- uploadWorkload(String path)

将指定路径下的工作负载加入系统

输入值：工作负载的文件路径

返回值：当前工作负载相关信息的字符串列表（工作负载的细节与结构）

返回值实例：

Details:

path:/Users/eclipse-workspace/mult/dataset/blog_dox.json

This is a doc data.

It contains 100000 nodes.

Configurations:

name: data1

eg:

{

    "id": "000001",

    "authorid": "02383",

    "topic": "美容",

    "date": "20170618",

    "blog": {

        "title": "mlxjfuzb",

        "key words": "ckwhslnpt",

        "content": "gPODMVbEqhWMDWRNAQW6xdulyDUVLKayn7NWzhIEivL130ttO3846fBlftd4WesClxHJxdlVjsPnDCWIr3PXOkQsEwxUQjRsoTkZElTvsX5XXOIEl0j9HFa2hK7Z1hKBAHd32yWuzXVUeBoYa3xNDL7wvT0JrcyPQEq0czjw5RBLtPqgS0iZnciaySwJQranmiDlt6NFPQxUIO2Vx4HeiiMxKNIFqUK0qYv0msbrFxq29P4EjKJPmc7Bk70PcMc7NHyRrSHx481ZMPX6Sko9t2v3wwcw41q8wYsiHhosQMhso4Bh75Y47i1JSdwqDKe4HaoaDn7sj9WyvAkSYfR5Vr38rmLW5zV1egfxpwjI5i0T2E2eK7oFs1BCUW4fal0NBctcd6gRygLJXPg7iGxDa22Qo1ne0It1GdB93bt70mCVb71Et0YzfiEjKWkyiPU6zcOyyzX1d6srujJtMHG4TEakkgVz7c6trBeEyaIVOWpuYnwPtTUbXVsSFcaZ0EFaz4gz8OOBFWF3ojBKZ8bMm2NMIHqNGwqar5xUuWl0LNgHBAEPYSMontnDx3MXDRZygQVEdPYRfzGkCxBiuOfi95OH9dvwpatdTVRtJ8zkdsyIi4im4l8nAr1zOn5GN21CGgSWfjIDW7U6P1NoZ5DUjxV9W6Gu42vfUJtlUbQlOfzQTdI5zsfaZn5XIGMF2Obf8rEsYpUb6c9TCVvIhkDkMPke7X94iikQtpfcC1nSKfNkaiEueZsIIzHJf6SclA7nAQYIkbIc594CAsXh8tUqdcsQg2JgY1hmzd1lWmQiGrk49DAZNFw4IUjl3rur9RZrlGn0KJqONoEdRBWSjUEZlLRKGdfQo9eNwOMKkrB8UvlkUoFxi5t0FSv1jOIUObYpKfP0XaVkqIxmCDGuIHrBksVjNOVuhX5V8uNEPB3IciRbA2yzpLshynnJzfjXutaUmi1ztZjCnirYpi7U5XEAflTlcELniAMO6cAMtnXiNj"

    }

}

The destination database is test.traincoll


- indexSelect(List<String> dataDetials, List<String> workloadDetials)

根据读入的文档数据与工作负载的内容来做索引推荐

输入值：加载文档数据和加载工作负载时的返回值

返回值：索引推荐结果以及性能测试的字符串列表

返回值实例：

The recommended index of fields under this load is as follows:

  date

		sparse b-tree index

  id

  	no index

  authorid

  	no index

  topic

  	no index

  blog.title

  	no index

  blog.key words

  	no index

  blog.content

  	no index

Smart method indexing performance increased by99.44773177657822%99.44773177657822
