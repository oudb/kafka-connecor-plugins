#kafka-connector-plugins

neo4j connector uber jar

1、get neo4j-kafka-connect-neo4j and unpack，then enter unpack directory
link：https://github.com/neo4j-contrib/neo4j-streams/releases/tag/4.1.2
you need download is neo4j-kafka-connect-neo4j-{version}-kc-oss.zip
for example neo4j-kafka-connect-neo4j-2.0.2-kc-oss.zip is 2.0.2 version

2、new a file named: build.gradle，the content is：

````
apply plugin: 'java'

jar {

    baseName "kafka-connect-neo4j-all-2.0.2"

    from files("lib2").collect { it.isDirectory() ? it : zipTree(it) }
}
````


3、new a file named: build.sh，the content is：
````
rm -rf  lib2
cp -rf lib lib2
cd lib2
for f in `find . -name '*.jar'`
do
echo $f
unzip -o $f
rm $f
done
cd ..
gradle build
````

4、run build.sh，and you find the uber jar in: build/libs/kafka-connect-neo4j-all-2.0.2.jar