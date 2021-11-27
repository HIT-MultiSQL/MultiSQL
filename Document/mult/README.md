# Document data section
### Document.java
-getTime()

Query the query time under the same set of loads under the three indexes (default, manual method, smart method);

Return value: long[], an array of query time under different indexes;

Throw exception types: UnknownHostException, ParseException;

<br/>

-getSingleQuery(String sql, int select)

Analyze the single-modal sql statement and complete the query;

Input value: query statement sql; choice of different indexes (0 is to build default index, 1 is to build manual recommendation index, 2 is to build only recommendation index)

Return value: List<String>, the list of query result ID

Throw exception types: UnknownHostException, ParseException;

<br/>

-getMultiQuery(String sql, int select)

Analyze multi-modal sql statements to complete the query;

Input value: query statement sql; choice of different indexes (0 is to build default index, 1 is to build manual recommendation index, 2 is to build only recommendation index)

Return value: List<String>, the list of query result ID

Throw exception types: UnknownHostException, ParseException;

### DocumentNew.java
The interface function is the same as Document.java, the internal implementation code is modified.

### JsonHandle.java
-jsonFormatter(String uglyJSONString)

Convert complex nested json string to path json string, which is convenient for sql query and use;

Input value: the original nested json string

Return value: unnested path json string

### QtFunc.java

-uploadData(String path)

Save the document data file under the specified path into the database

Input value: the path of the document data json file

Return value: String list of current document data related information (details of document data and structure of document data)

Examples of return values:

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

-uploadWorkload(String path)

Add the workload under the specified path to the system

Input value: file path of the workload

Return value: String list of current workload related information (workload details and structure)

Examples of return values:

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

    "topic": "Beauty",

    "date": "20170618",

    "blog": {

        "title": "mlxjfuzb",

        "key words": "ckwhslnpt",

        "Content": "gPODMVbEqhWMDWRNAQW6xdulyDUVLKayn7NWzhIEivL130ttO3846fBlftd4WesClxHJxdlVjsPnDCWIr3PXOkQsEwxUQjRsoTkZElTvsX5XXOIEl0j9HFa2hK7Z1hKBAHd32yWuzXVUeBoYa3xNDL7wvT0JrcyPQEq0czjw5RBLtPqgS0iZnciaySwJQranmiDlt6NFPQxUIO2Vx4HeiiMxKNIFqUK0qYv0msbrFxq29P4EjKJPmc7Bk70PcMc7NHyRrSHx481ZMPX6Sko9t2v3wwcw41q8wYsiHhosQMhso4Bh75Y47i1JSdwqDKe4HaoaDn7sj9WyvAkSYfR5Vr38rmLW5zV1egfxpwjI5i0T2E2eK7oFs1BCUW4fal0NBctcd6gRygLJXPg7iGxDa22Qo1ne0It1GdB93bt70mCVb71Et0YzfiEjKWkyiPU6zcOyyzX1d6srujJtMHG4TEakkgVz7c6trBeEyaIVOWpuYnwPtTUbXVsSFcaZ0EFaz4gz8OOBFWF3ojBKZ8bMm2NMIHqNGwqar5xUuWl0LNgHBAEPYSMontnDx3MXDRZygQVEdPYRfzGkCxBiuOfi95OH9dvwpatdTVRtJ8zkdsyIi4im4l8nAr1zOn5GN21CGgSWfjIDW7U6P1NoZ5DUjxV9W6Gu42vfUJtlUbQlOfzQTdI5zsfaZn5XIGMF2Obf8rEsYpUb6c9TCVvIhkDkMPke7X94iikQtpfcC1nSKfNkaiEueZsIIzHJf6SclA7nAQYIkbIc594CAsXh8tUqdcsQg2JgY1hmzd1lWmQiGrk49DAZNFw4IUjl3rur9RZrlGn0KJqONoEdRBWSjUEZlLRKGdfQo9eNwOMKkrB8UvlkUoFxi5t0FSv1jOIUObYpKfP0XaVkqIxmCDGuIHrBksVjNOVuhX5V8uNEPB3IciRbA2yzpLshynnJzfjXutaUmi1ztZjCnirYpi7U5XEAflTlcELn iAMO6cAMtnXiNj"

    }

}

The destination database is test.traincoll


-indexSelect(List<String> dataDetials, List<String> workloadDetials)

Make index recommendations based on the read document data and the content of the workload

Input value: the return value when loading document data and loading workload

Return value: Index recommendation result and string list of performance test

Examples of return values:

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
