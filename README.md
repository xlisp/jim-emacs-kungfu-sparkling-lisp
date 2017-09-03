
# Clojure Sparkling & statistics, machine learning, kungfu
* 一个打十几个人, 甚至都拿刀的高手，分类处理。打败弱的对手先，最后打最强的高手，必须先听桥每个对手的弱点 ，中线在哪里，怎样弱点才能打败他的中线



- [Clojure Sparkling & statistics, machine learning, kungfu](#clojure-sparkling--statistics-machine-learning-kungfu)
    - [Spark context](#spark-context)
    - [Spark Streaming context](#spark-streaming-context)
    - [Socket Text Stream](#socket-text-stream)
    - [Stream hello-world print整个数据流](#stream-hello-world-print%E6%95%B4%E4%B8%AA%E6%95%B0%E6%8D%AE%E6%B5%81)
    - [Kafka Stream](#kafka-stream)
    - [Foreach RDD](#foreach-rdd)
    - [tuple and untuple](#tuple-and-untuple)
    - [线性回归SGD](#%E7%BA%BF%E6%80%A7%E5%9B%9E%E5%BD%92sgd)
    - [贝叶斯](#%E8%B4%9D%E5%8F%B6%E6%96%AF)
    - [ALS交替最小二乘法的协同过滤算法--推荐引擎学习](#als%E4%BA%A4%E6%9B%BF%E6%9C%80%E5%B0%8F%E4%BA%8C%E4%B9%98%E6%B3%95%E7%9A%84%E5%8D%8F%E5%90%8C%E8%BF%87%E6%BB%A4%E7%AE%97%E6%B3%95--%E6%8E%A8%E8%8D%90%E5%BC%95%E6%93%8E%E5%AD%A6%E4%B9%A0)
    - [随机模拟,随机树到随机森林和功夫的骗手，用骗手来知其真](#%E9%9A%8F%E6%9C%BA%E6%A8%A1%E6%8B%9F%E9%9A%8F%E6%9C%BA%E6%A0%91%E5%88%B0%E9%9A%8F%E6%9C%BA%E6%A3%AE%E6%9E%97%E5%92%8C%E5%8A%9F%E5%A4%AB%E7%9A%84%E9%AA%97%E6%89%8B%E7%94%A8%E9%AA%97%E6%89%8B%E6%9D%A5%E7%9F%A5%E5%85%B6%E7%9C%9F)
    - [svm升维度，敌人分类，然后降维度](#svm%E5%8D%87%E7%BB%B4%E5%BA%A6%E6%95%8C%E4%BA%BA%E5%88%86%E7%B1%BB%E7%84%B6%E5%90%8E%E9%99%8D%E7%BB%B4%E5%BA%A6)
    - [每一个攻防招式都是高阶函数](#%E6%AF%8F%E4%B8%80%E4%B8%AA%E6%94%BB%E9%98%B2%E6%8B%9B%E5%BC%8F%E9%83%BD%E6%98%AF%E9%AB%98%E9%98%B6%E5%87%BD%E6%95%B0)
    - [组合拳或者腿就是组合函数](#%E7%BB%84%E5%90%88%E6%8B%B3%E6%88%96%E8%80%85%E8%85%BF%E5%B0%B1%E6%98%AF%E7%BB%84%E5%90%88%E5%87%BD%E6%95%B0)
    - [能够和你黐手的朋友才是真正的朋友](#%E8%83%BD%E5%A4%9F%E5%92%8C%E4%BD%A0%E9%BB%90%E6%89%8B%E7%9A%84%E6%9C%8B%E5%8F%8B%E6%89%8D%E6%98%AF%E7%9C%9F%E6%AD%A3%E7%9A%84%E6%9C%8B%E5%8F%8B)
    - [一个打十几个人的能力，打一百万人的能力，从身边的人打起爸爸，妈妈，姐](#%E4%B8%80%E4%B8%AA%E6%89%93%E5%8D%81%E5%87%A0%E4%B8%AA%E4%BA%BA%E7%9A%84%E8%83%BD%E5%8A%9B%E6%89%93%E4%B8%80%E7%99%BE%E4%B8%87%E4%BA%BA%E7%9A%84%E8%83%BD%E5%8A%9B%E4%BB%8E%E8%BA%AB%E8%BE%B9%E7%9A%84%E4%BA%BA%E6%89%93%E8%B5%B7%E7%88%B8%E7%88%B8%E5%A6%88%E5%A6%88%E5%A7%90)
    - [一切都是功夫，一切都是高阶函数，皆可打出去](#%E4%B8%80%E5%88%87%E9%83%BD%E6%98%AF%E5%8A%9F%E5%A4%AB%E4%B8%80%E5%88%87%E9%83%BD%E6%98%AF%E9%AB%98%E9%98%B6%E5%87%BD%E6%95%B0%E7%9A%86%E5%8F%AF%E6%89%93%E5%87%BA%E5%8E%BB)


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
### ALS交替最小二乘法的协同过滤算法--推荐引擎学习
```clojure
(defn to-mllib-rdd [rdd]
  (.rdd rdd))
(defn alternating-least-squares [data {:keys [rank num-iter lambda]}]
  (ALS/train (to-mllib-rdd data) rank num-iter lambda 10))
(defn parse-ratings [sc]
  (->> (spark/text-file sc "resources/data/ml-100k/ua.base")
       (spark/map-to-pair parse-rating)))
(defn training-ratings [ratings]
  (->> ratings
       (spark/filter (fn [tuple]
                       (< (s-de/key tuple) 8)))
       (spark/values)))

(let [options {:rank 10
               :num-iter 10
               :lambda 1.0}
      model (-> (parse-ratings sc)
                (training-ratings)
                (alternating-least-squares options))]
  (into [] (.recommendProducts model 1 3)))

(.predict model 789 123) ;; 预测用户789,对电影123的评分 ;;=> 2.401917277364834

(into [] (.recommendProducts model 789 5)) ;;=> 给用户789,推荐5个电影
;; Rating(789,814,3.7114404312220763)
;; Rating(789,1500,3.642514446544692) ... 
;; Rating(789,1449,3.484917824309928)
```
### 随机模拟,随机树到随机森林和功夫的骗手，用骗手来知其真
```clojure
```
### svm升维度，敌人分类，然后降维度
```clojure
```
### 每一个攻防招式都是高阶函数
```clojure
```
### 组合拳或者腿就是组合函数
```clojure
```
### 能够和你黐手的朋友才是真正的朋友
```clojure
```
### 一个打十几个人的能力，打一百万人的能力，从身边的人打起爸爸，妈妈，姐
```clojure
```
### 一切都是功夫，一切都是高阶函数，皆可打出去 
```clojure
```
