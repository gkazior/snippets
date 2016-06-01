    
    %sh
    wget http://en.wikipedia.org/wiki/Hortonworks
    
    %sh
    hadoop fs -put ~/Hortonworks /tmp
    
    
    %pyspark
    myLines = sc.textFile('hdfs://sandbox.hortonworks.com/tmp/Hortonworks')
    myLinesFiltered = myLines.filter( lambda x: len(x) > 0 )
    count = myLinesFiltered.count()
    print count
    
    // tutorial on pyspark is not working - here scala version 
    val file1 = sc.textFile("hdfs://sandbox.hortonworks.com/tmp/Hortonworks")
    val filtered = file1.filter(_.length > 0)
    val count = filtered.count
    println(s"Found $count")
