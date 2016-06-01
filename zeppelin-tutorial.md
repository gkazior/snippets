# First tutorial    
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



# Tutorial on zeppelin

    %sh
    rm ~/bank.zip
    rm -rf  ~/data
    cd ~
    wget http://archive.ics.uci.edu/ml/machine-learning-databases/00222/bank.zip
    mkdir data
    unzip bank.zip -d data
    rm bank.zip

    hadoop fs -put  ~/data/bank-full.csv .
    hadoop fs -ls -h bank-full.csv
    
    
    //import sys.process._
    // sc is an existing SparkContext.
    val sqlContext = new org.apache.spark.sql.SQLContext(sc)


    val bankText = sc.textFile("bank-full.csv")

    case class Bank(age: Integer, job: String, marital: String, education: String, balance: Integer)

    val bank = bankText.map(s => s.split(";")).filter(s => s(0) != "\"age\"").map(
        s => Bank(s(0).toInt, 
            s(1).replaceAll("\"", ""),
            s(2).replaceAll("\"", ""),
            s(3).replaceAll("\"", ""),
            s(5).replaceAll("\"", "").toInt
        )
    )
    // toDF() works only in spark 1.3.0.
    // For spark 1.1.x and spark 1.2.x,
    // use below instead:
    // bank.registerTempTable("bank"
    bank.toDF().registerTempTable("bank")


    %sql 
    select age, count(1) value, sum(balance)
    from bank 
    where age < 50 
    group by age 
    order by age
    
    %sql 
    select age, count(1) value 
    from bank 
    where marital="${marital=single,single|divorced|married}" 
    group by age 
    order by age
    
    %sql 
    /* on the same dataset average age depending on marital ;-) */
    select marital, avg(age) avg_age 
    from bank 
    group by marital 
    order by avg_age desc
    /**
    Gives:
    marital	avg_age
    divorced	45.78298444401767
    married	    43.40809877269053
    single	    33.7034401876466
    */
    
