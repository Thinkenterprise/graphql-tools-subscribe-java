# About
graphql-tools-subscribe-java is the **Java** implementation of the **JavaScript** graphql-tools-subscribe reference implementation. 
The documentation of the reference implementation can be found at  (https://github.com/rse/graphql-tools-subscribe). 

# Installation
## Maven 

```
mvn clean install
```

## Gradle 

FIXME

# Usage 

## Maven 
```
<dependency>
	<groupId>com.graphqlio</groupId>
	<artifactId>graphql-tools-subscribe-java</artifactId>
	<version>0.0.9</version>
</dependency>

```

## Gradle 

```
dependencies {
  compile 'com.graphqlio:graphql-tools-subscribe-java:0.0.9'
}
```


# Sample 

working with GtsRecord:

``` java
		GtsRecord record = GtsRecord.builder().op(GtsOperationType.READ)
				.arity(GtsArityType.ONE)
				.dstType("dstType")
				.dstIds(new String[] {"dstId1", "dstId2"})
				.dstAttrs(new String[] {"dstAttr1", "dstAttr2"})
				.build();

		String strRecord = record.stringify();

		GtsRecord recordFromString =
				GtsRecord.builder().stringified(strRecord).build();
```


working with GtsEvaluation:

``` java
	@Autowired
	GtsEvaluation graphQLIOEvaluation;

	String strRecordQuerySid1 =
			"read(many)->item{id1,id2,id3,id4,id5}.{id,name,address,email}";

	GtsRecord recordRecordQuerySid1 =
			GtsRecord.builder().stringified(strRecordQuerySid1).build();

	GtsScope scopeSid1Cid1 =
			GtsScope.builder().withScopeId("Sid1").withConnectionId("Cid1").withQuery(strRecordQuerySid1).withState(GtsScopeState.SUBSCRIBED).build();

	scopeSid1Cid1.addRecord(recordRecordQuerySid1);
	scopeSid1Cid1.addRecord(recordMutationUpdateItemInQuerySid1);

	List<String> outdatedSids =
			graphQLIOEvaluation.evaluateOutdatedSids(scopeSid1Cid1);
```


working with GtsKeyValueStore:

``` java
	@Autowired
	GtsKeyValueStore kvp;

	kvp.start();

	kvp.store("cid1", "sid1", "Value for <cid1,sid1>");
	boolean bool = kvp.hasKey("cid1", "sid1");
	String value = kvp.get("cid1", "sid1");
	Set<String> allKeys = kvp.getAllKeys();
	Set<String> allKeysCid = kvp.getAllKeysForConnection("cid1");
	Set<String> allKeysSid = kvp.getAllKeysForScope("sid1");
	kvp.delete("cid1", "sid1");

	kvp.stop();
```


# License 
Design and Development by msg Applied Technology Research
Copyright (c) 2019-2020 msg systems ag (http://www.msg-systems.com/)
All Rights Reserved.
 
Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
"Software"), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:
 
The above copyright notice and this permission notice shall be included
in all copies or substantial portions of the Software.
 
THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.