# jim-emacs-fun-sparkling-lisp

### flambo: spark streaming
```clojure
(ns flambo-example.core
  (:require [flambo.conf :as conf]
            [flambo.api :as api]
            [flambo.function :as function]
            [flambo.streaming :as streaming]
            [clojure.tools.logging :as log])
  (:import [org.apache.spark.streaming.api.java JavaStreamingContext]
           [org.apache.spark.streaming.receiver Receiver]
           [org.apache.spark.storage StorageLevel]
           [org.apache.kafka.common.serialization StringSerializer]
           [org.apache.kafka.clients.producer KafkaProducer ProducerRecord Callback RecordMetadata]
           [java.util Map])
  (:gen-class))

(defn num-range-receiver
  [n]
  (proxy [Receiver] [(StorageLevel/MEMORY_AND_DISK_2)]
    (onStart []
      (require '[clojure.tools.logging :as log]) ;; required, otherwise there's unbound var exception
      (log/info "Starting receiver")
      (future
        (doseq [x (range 1 n)]
          (log/info (str "Store: " x))
          (.store this x)
          (Thread/sleep (rand-int 500)))))
    (onStop [] (log/info "Stopping receiver"))))

(api/defsparkfn fizzbuzz [x]
  (let [r (cond
            (zero? (mod x 15)) "FizzBuzz"
            (zero? (mod x 5)) "Buzz"
            (zero? (mod x 3)) "Fizz"
            :else x)]
    (str [x r])))

(api/defsparkfn publish-using-partitions [rdd _]
  (.foreachPartition
   rdd
   (function/void-function
    (api/fn [xs]
      (doseq [x (iterator-seq xs)]
        (log/info (str "---->>> Sending to Kafka fizzbuzz " x " , " (type x) ))
        (send! (memoized-producer producer-config) "fizzbuzz" x (->callback x)))))))

(def env {"spark.executor.memory" "1G"
          "spark.files.overwrite" "true"})

(def c (-> (conf/spark-conf)
           (conf/master "local[*]")
           (conf/app-name "flambo-custom-receiver-kafka-eample")
           (conf/set "spark.akka.timeout" "1000")
           (conf/set-executor-env env)))

(defn -main [& [n]]
  (let [ssc (streaming/streaming-context c 10000)
        stream (.receiverStream ^JavaStreamingContext ssc (num-range-receiver (Integer/parseInt n)))]
    (-> stream
        (streaming/map fizzbuzz)
        (streaming/foreach-rdd publish-using-partitions))
    (.start ssc)
    (.awaitTerminationOrTimeout ssc 90000)))  
```

### powderkeg: spark sql
```clojure
(ns powderkeg-example.sql
  (:require
   [powderkeg.core :as keg]
   [net.cgrand.xforms :as x])
  (:import
   [org.apache.spark.sql SparkSession SQLContext]
   [org.apache.spark.sql.types StringType StructField StructType]
   [org.apache.spark.sql.types DataTypes]
   [org.apache.spark.sql Row SaveMode RowFactory]))

(keg/connect! "local")

(def customer
  (let [txtf (.textFile keg/*sc* "/Users/stevechan/Downloads/2000W/*.csv")
        maped-rdd (keg/rdd
                   txtf
                   (map #(clojure.string/split % #",") )
                   (filter #(> (count %) 7) )
                   (map
                    #(RowFactory/create
                      (into-array
                       (mapv % [0 5 4 6 7])
                       ))) (distinct))]
    (.createDataFrame
     (->> keg/*sc* .sc (new SparkSession))
     maped-rdd
     (DataTypes/createStructType
      (map #(DataTypes/createStructField % DataTypes/StringType false)
           ["name" "gender" "ctfId" "birthday" "address"]) ) )))
           
(comment
  (.createOrReplaceTempView customer "customer")
  (.show
   (.sql
    (->> keg/*sc* .sc (new SQLContext))
    "SELECT * FROM customer where address like '%北京市%'" )))
```
