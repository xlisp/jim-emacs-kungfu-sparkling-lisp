# Clojure Sparkling & statistics, machine learning list

### Spark context
```clojure
(spark/with-context context
  (-> (conf/spark-conf)
      (conf/master "local[*]")
      (conf/app-name "Consumer"))
  (do ... ))
```
### Spark Streaming context
```clojure
(let [streaming-context (JavaStreamingContext. context (Duration. 1000))
     ... ]
  (do ... ))
```
### Socket Text Stream
```clojure
(def socket-stream (.socketTextStream streaming-context "localhost" 9999))
```
### Stream hello-world print整个数据流
```clojure
(defn -main
  [& args]
  (do
    (.print socket-stream) ;; 或者是其它流, 如Kafka
    (.start streaming-context)
    (.awaitTermination streaming-context)))
```
### Kafka Stream
```clojure
(let [parameters (HashMap. {"metadata.broker.list" "127.0.0.1:9092"})
      topics (Collections/singleton "abc_messages")
      stream (KafkaUtils/createDirectStream streaming-context String String StringDecoder StringDecoder parameters topics)
     ... ]
  (do ... ))
```
### Foreach RDD
```clojure
(defn foreach-rdd [dstream f]
  (.foreachRDD dstream (function2 f)))
```
### tuple and untuple
```clojure
(spark/map-to-pair
 (fn [lp]
   (spark/tuple (.label lp) (.features lp)))
 labeled-stream)

(defn untuple [^Tuple2 t]
  (persistent!
   (conj!
    (conj! (transient []) (._1 t))
    (._2 t))))
```
### 线性回归
```clojure
```
### 贝叶斯
```clojure
```
