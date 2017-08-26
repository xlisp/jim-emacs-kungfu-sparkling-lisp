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
### 线性回归SGD
```java
public static StreamingLinearRegressionWithSGD linearRegressionodel(double [] args, int num, float size) {
    StreamingLinearRegressionWithSGD model = new StreamingLinearRegressionWithSGD()
        .setStepSize(size)
        .setNumIterations(num)
        .setInitialWeights(Vectors.dense(args));
    return model;
}
public static LabeledPoint labeledPoint(double label, double [] args) {
    LabeledPoint point = new LabeledPoint(label, Vectors.dense(args));
    return point;
}
```
```clojure
(def model (VectorClojure/linearRegressionodel (double-array (repeat 100 0.0)) 1 0.01))
(def labeled-stream
  (spark/map
   (fn [record]
     (let [split (clojure.string/split record #"\t")
           y (Double/parseDouble (nth split 0))
           features (-> (nth split 1) (clojure.string/split #",") ((fn [fs] (map #(Double/parseDouble %) fs))) double-array)]
       (VectorClojure/labeledPoint y features))) stream))
(do
  (.trainOn model labeled-stream)
  (.print
   (.predictOnValues
    model
    (spark/map-to-pair
     (fn [lp]
       (spark/tuple (.label lp) (.features lp)))
     labeled-stream)))
  (do ... start ...))
```
### 贝叶斯
```java
public static Vector tftransform(HashingTF tf, String data) {
    Vector tfres = tf.transform(Arrays.asList(data.split(" ")));
    return tfres;
}
```
```clojure
(let [spam (spark/text-file context "files/spam.txt")
      ham (spark/text-file context "files/ham.txt")
      tf (HashingTF. 100)
      spam-features (spark/map (fn [x] (VectorClojure/tftransform tf x)) spam)
      ham-features (spark/map (fn [x] (VectorClojure/tftransform tf x)) ham)
      positive-examples (spark/map (fn [x] (LabeledPoint. 1 x)) spam-features)
      negative-examples (spark/map (fn [x] (LabeledPoint. 0 x)) ham-features)
      training-data (spark/union (.rdd positive-examples) (.rdd negative-examples))
      model (NaiveBayes/train training-data 1.0)
      predict (fn [x] (.predict model (VectorClojure/tftransform tf x)))]
  (do ... ))
```
