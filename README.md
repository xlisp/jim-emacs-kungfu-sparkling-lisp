

# Clojure Sparkling & statistics, machine learning, kungfu
* 一个打十几个人, 甚至都拿刀的高手，分类处理。打败弱的对手先，最后打最强的高手，必须先听桥每个对手的弱点 ，中线在哪里，怎样弱点才能打败他的中线

- [Clojure Sparkling & statistics, machine learning, kungfu](#clojure-sparkling--statistics-machine-learning-kungfu)
    - [Spark context](#spark-context)
    - [Spark Streaming context](#spark-streaming-context)
    - [Socket Text Stream](#socket-text-stream)
    - [Spark的闭包的处理是关键,Clojure与Spark互操作的关键: 函数的序列化](#spark%E7%9A%84%E9%97%AD%E5%8C%85%E7%9A%84%E5%A4%84%E7%90%86%E6%98%AF%E5%85%B3%E9%94%AEclojure%E4%B8%8Espark%E4%BA%92%E6%93%8D%E4%BD%9C%E7%9A%84%E5%85%B3%E9%94%AE-%E5%87%BD%E6%95%B0%E7%9A%84%E5%BA%8F%E5%88%97%E5%8C%96)
    - [函数式操作的核心,SICP的原力爆发: map reduce](#%E5%87%BD%E6%95%B0%E5%BC%8F%E6%93%8D%E4%BD%9C%E7%9A%84%E6%A0%B8%E5%BF%83sicp%E7%9A%84%E5%8E%9F%E5%8A%9B%E7%88%86%E5%8F%91-map-reduce)
    - [Clojure和Scala的互操作: tuple and untuple](#clojure%E5%92%8Cscala%E7%9A%84%E4%BA%92%E6%93%8D%E4%BD%9C-tuple-and-untuple)
    - [Stream hello-world print整个数据流](#stream-hello-world-print%E6%95%B4%E4%B8%AA%E6%95%B0%E6%8D%AE%E6%B5%81)
    - [Kafka Stream](#kafka-stream)
    - [Spark SQL](#spark-sql)
    - [Foreach RDD](#foreach-rdd)
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
    - [一对多个分布式对手，是分布式的数据源数据流，攻防的组合招式是数据流的管道](#%E4%B8%80%E5%AF%B9%E5%A4%9A%E4%B8%AA%E5%88%86%E5%B8%83%E5%BC%8F%E5%AF%B9%E6%89%8B%E6%98%AF%E5%88%86%E5%B8%83%E5%BC%8F%E7%9A%84%E6%95%B0%E6%8D%AE%E6%BA%90%E6%95%B0%E6%8D%AE%E6%B5%81%E6%94%BB%E9%98%B2%E7%9A%84%E7%BB%84%E5%90%88%E6%8B%9B%E5%BC%8F%E6%98%AF%E6%95%B0%E6%8D%AE%E6%B5%81%E7%9A%84%E7%AE%A1%E9%81%93)
    - [功夫中的双截棍等武器，是数据流管道的用的帮助工具](#%E5%8A%9F%E5%A4%AB%E4%B8%AD%E7%9A%84%E5%8F%8C%E6%88%AA%E6%A3%8D%E7%AD%89%E6%AD%A6%E5%99%A8%E6%98%AF%E6%95%B0%E6%8D%AE%E6%B5%81%E7%AE%A1%E9%81%93%E7%9A%84%E7%94%A8%E7%9A%84%E5%B8%AE%E5%8A%A9%E5%B7%A5%E5%85%B7)
    - [咏春分手(小念头的分手在第二段，寻桥分手加了转马)，手像两个盾牌一样，攻击连消带打 ，来留去送 ，甩手直冲。。。而不是他打我，我后退马，只是防御 ，没有攻击的防御是没用的 => 分手训练，小念头和寻桥分手训练，一手标一伏，发力为一体的两手，而不是分裂的，但是分工不一样](#%E5%92%8F%E6%98%A5%E5%88%86%E6%89%8B%E5%B0%8F%E5%BF%B5%E5%A4%B4%E7%9A%84%E5%88%86%E6%89%8B%E5%9C%A8%E7%AC%AC%E4%BA%8C%E6%AE%B5%E5%AF%BB%E6%A1%A5%E5%88%86%E6%89%8B%E5%8A%A0%E4%BA%86%E8%BD%AC%E9%A9%AC%E6%89%8B%E5%83%8F%E4%B8%A4%E4%B8%AA%E7%9B%BE%E7%89%8C%E4%B8%80%E6%A0%B7%E6%94%BB%E5%87%BB%E8%BF%9E%E6%B6%88%E5%B8%A6%E6%89%93-%E6%9D%A5%E7%95%99%E5%8E%BB%E9%80%81-%E7%94%A9%E6%89%8B%E7%9B%B4%E5%86%B2%E8%80%8C%E4%B8%8D%E6%98%AF%E4%BB%96%E6%89%93%E6%88%91%E6%88%91%E5%90%8E%E9%80%80%E9%A9%AC%E5%8F%AA%E6%98%AF%E9%98%B2%E5%BE%A1-%E6%B2%A1%E6%9C%89%E6%94%BB%E5%87%BB%E7%9A%84%E9%98%B2%E5%BE%A1%E6%98%AF%E6%B2%A1%E7%94%A8%E7%9A%84--%E5%88%86%E6%89%8B%E8%AE%AD%E7%BB%83%E5%B0%8F%E5%BF%B5%E5%A4%B4%E5%92%8C%E5%AF%BB%E6%A1%A5%E5%88%86%E6%89%8B%E8%AE%AD%E7%BB%83%E4%B8%80%E6%89%8B%E6%A0%87%E4%B8%80%E4%BC%8F%E5%8F%91%E5%8A%9B%E4%B8%BA%E4%B8%80%E4%BD%93%E7%9A%84%E4%B8%A4%E6%89%8B%E8%80%8C%E4%B8%8D%E6%98%AF%E5%88%86%E8%A3%82%E7%9A%84%E4%BD%86%E6%98%AF%E5%88%86%E5%B7%A5%E4%B8%8D%E4%B8%80%E6%A0%B7)
    - [离开我中线，非中线向前，就可以出击 ，用黐手的打来提醒训练，发力错误，肘低发力 肩膀放松 归中三角形结构力 攻防才能奏效](#%E7%A6%BB%E5%BC%80%E6%88%91%E4%B8%AD%E7%BA%BF%E9%9D%9E%E4%B8%AD%E7%BA%BF%E5%90%91%E5%89%8D%E5%B0%B1%E5%8F%AF%E4%BB%A5%E5%87%BA%E5%87%BB-%E7%94%A8%E9%BB%90%E6%89%8B%E7%9A%84%E6%89%93%E6%9D%A5%E6%8F%90%E9%86%92%E8%AE%AD%E7%BB%83%E5%8F%91%E5%8A%9B%E9%94%99%E8%AF%AF%E8%82%98%E4%BD%8E%E5%8F%91%E5%8A%9B-%E8%82%A9%E8%86%80%E6%94%BE%E6%9D%BE-%E5%BD%92%E4%B8%AD%E4%B8%89%E8%A7%92%E5%BD%A2%E7%BB%93%E6%9E%84%E5%8A%9B-%E6%94%BB%E9%98%B2%E6%89%8D%E8%83%BD%E5%A5%8F%E6%95%88)
    - [离开我就打他，叫甩手直冲](#%E7%A6%BB%E5%BC%80%E6%88%91%E5%B0%B1%E6%89%93%E4%BB%96%E5%8F%AB%E7%94%A9%E6%89%8B%E7%9B%B4%E5%86%B2)
    - [来留去送 ，就像放风筝一样，顺着他的力 然后打他，如他向前较劲就拉打，他拉我就 我就撞打他](#%E6%9D%A5%E7%95%99%E5%8E%BB%E9%80%81-%E5%B0%B1%E5%83%8F%E6%94%BE%E9%A3%8E%E7%AD%9D%E4%B8%80%E6%A0%B7%E9%A1%BA%E7%9D%80%E4%BB%96%E7%9A%84%E5%8A%9B-%E7%84%B6%E5%90%8E%E6%89%93%E4%BB%96%E5%A6%82%E4%BB%96%E5%90%91%E5%89%8D%E8%BE%83%E5%8A%B2%E5%B0%B1%E6%8B%89%E6%89%93%E4%BB%96%E6%8B%89%E6%88%91%E5%B0%B1-%E6%88%91%E5%B0%B1%E6%92%9E%E6%89%93%E4%BB%96)
    - [生活中的中线原理和埋肘原理，守中用中: 归中  和 连消带打 111 用在朋友和高人身上一样奏效，父母身上，创造咏春拳的人 ，才是绝世大师，中线原理](#%E7%94%9F%E6%B4%BB%E4%B8%AD%E7%9A%84%E4%B8%AD%E7%BA%BF%E5%8E%9F%E7%90%86%E5%92%8C%E5%9F%8B%E8%82%98%E5%8E%9F%E7%90%86%E5%AE%88%E4%B8%AD%E7%94%A8%E4%B8%AD-%E5%BD%92%E4%B8%AD--%E5%92%8C-%E8%BF%9E%E6%B6%88%E5%B8%A6%E6%89%93-111-%E7%94%A8%E5%9C%A8%E6%9C%8B%E5%8F%8B%E5%92%8C%E9%AB%98%E4%BA%BA%E8%BA%AB%E4%B8%8A%E4%B8%80%E6%A0%B7%E5%A5%8F%E6%95%88%E7%88%B6%E6%AF%8D%E8%BA%AB%E4%B8%8A%E5%88%9B%E9%80%A0%E5%92%8F%E6%98%A5%E6%8B%B3%E7%9A%84%E4%BA%BA-%E6%89%8D%E6%98%AF%E7%BB%9D%E4%B8%96%E5%A4%A7%E5%B8%88%E4%B8%AD%E7%BA%BF%E5%8E%9F%E7%90%86)
    - [近邻分类(KNN)](#%E8%BF%91%E9%82%BB%E5%88%86%E7%B1%BBknn)
    - [朴素贝叶斯分类](#%E6%9C%B4%E7%B4%A0%E8%B4%9D%E5%8F%B6%E6%96%AF%E5%88%86%E7%B1%BB)
    - [决策树分类](#%E5%86%B3%E7%AD%96%E6%A0%91%E5%88%86%E7%B1%BB)
    - [预测数值型数据: 广义回归方法](#%E9%A2%84%E6%B5%8B%E6%95%B0%E5%80%BC%E5%9E%8B%E6%95%B0%E6%8D%AE-%E5%B9%BF%E4%B9%89%E5%9B%9E%E5%BD%92%E6%96%B9%E6%B3%95)
    - [神经网络和支持向量机](#%E7%A5%9E%E7%BB%8F%E7%BD%91%E7%BB%9C%E5%92%8C%E6%94%AF%E6%8C%81%E5%90%91%E9%87%8F%E6%9C%BA)
    - [K均值聚类](#k%E5%9D%87%E5%80%BC%E8%81%9A%E7%B1%BB)


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
### Spark 的矩阵计算(linalg+breeze)
```clojure
(def vec (Vectors/dense (double-array (list 0.1 0.15 0.2 0.3 0.25))))

(def mat (Matrices/dense 3 2 (double-array (list 1.0 3.0 5.0 2.0 4.0 6.0))))

(def sm (Matrices/sparse 3 2 (int-array (list 0 1 3)) (int-array (list 0 2 1)) (double-array (list 9 6 8))))

(def sv (Vectors/sparse 3 (int-array (list 0 2)) (double-array (list 1.0 3.0))))

(def pos (LabeledPoint. 1.0 (Vectors/dense (double-array (list 1.0 0.0 3.0)))))

(def mat-t (.transpose mat))

(def mat-multiply (.multiply mat mat-t))
;; => #object[org.apache.spark.mllib.linalg.DenseMatrix 0x63608adf "5.0   11.0  17.0  \n11.0  25.0  39.0  \n17.0  39.0  61.0  "]

;; Distributed matrix
(spark/with-context sc
  (-> (conf/spark-conf)
      (conf/master "local[*]")
      (conf/app-name "Consumer"))
  (let [data (Arrays/asList (into-array (list 1 2 3 4 5 6)))
        rdd-dist-data (.parallelize sc data)
        mat (RowMatrix. (.rdd rdd-dist-data))
        mat2 (IndexedRowMatrix. (.rdd rdd-dist-data))
        row-mat (.toRowMatrix mat2)]
    ;;(list (.numRows mat) (.numCols mat))
    (.numRows mat) ;;=> 6
    ))
```
### Spark的闭包的处理是关键,Clojure与Spark互操作的关键: 函数的序列化
* Sparkling的数据流操作都必须在with-context下,否则会报序列化的错误
* 而且Spark版本的问题也可能导致序列化和闭包的错误
```java
import clojure.lang.IFn;
public class Function2 extends sparkling.serialization.AbstractSerializableWrappedIFn implements org.apache.spark.api.java.function.Function2, org.apache.spark.sql.api.java.UDF2 {
    public Function2(IFn func) {
        super(func);
    }
    public Object call(Object v1, Object v2) throws Exception {
    return f.invoke(v1, v2);
  }
}
```
```clojure
(gen-function Function function)
(gen-function Function2 function2)
(gen-function Function3 function3)
(gen-function VoidFunction void-function)
(gen-function FlatMapFunction flat-map-function)
(gen-function FlatMapFunction2 flat-map-function2)
(gen-function PairFlatMapFunction pair-flat-map-function)
(gen-function PairFunction pair-function)
```
```clojure
(defn foreach-rdd [dstream f]
  (.foreachRDD dstream (function2 f)))
(foreach-rdd
 stream
 (fn [rdd arg2] ...))
```
### 函数式操作的核心,SICP的原力爆发: map reduce
```clojure
(defn map
  [f rdd]
  (-> (.map rdd (function f))
      (u/set-auto-name (u/unmangle-fn f))))
(defn map-to-pair
  [f rdd]
  (-> (.mapToPair rdd (pair-function f))
      (u/set-auto-name (u/unmangle-fn f))))
(defn reduce
  [f rdd]
  (u/set-auto-name (.reduce rdd (function2 f)) (u/unmangle-fn f)))
(defn foreach-partition
  [f rdd]
  (.foreachPartition rdd (void-function (comp f iterator-seq))))
(defn partition-by
  [^Partitioner partitioner ^JavaPairRDD rdd]
  (.partitionBy rdd partitioner))
```
### Clojure和Scala的互操作: tuple and untuple
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
### Spark SQL
* TODOS: 改写4G数据记录的Spark查询
```clojure
(defn select
  [cols data-frame]
  (.select data-frame
           (into-array cols)))
(defn where
  "call where by "
  [expression data-frame]
  (.where data-frame expression))

```
### Foreach RDD
```clojure
(defn foreach-rdd [dstream f]
  (.foreachRDD dstream (function2 f)))
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
(defn tftransform
  [tf x]
  (.transform tf (-> x (clojure.string/split #" ") into-array Arrays/asList)))

(let [spam (spark/text-file context "files/spam.txt")
      ham (spark/text-file context "files/ham.txt")
      tf (HashingTF. 100)
      spam-features (spark/map (fn [x] (tftransform tf x)) spam)
      ham-features (spark/map (fn [x] (tftransform tf x)) ham)
      positive-examples (spark/map (fn [x] (LabeledPoint. 1 x)) spam-features)
      negative-examples (spark/map (fn [x] (LabeledPoint. 0 x)) ham-features)
      training-data (spark/union (.rdd positive-examples) (.rdd negative-examples))
      model (NaiveBayes/train training-data 1.0)
      predict (fn [x] (.predict model (tftransform tf x)))]
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
### 一对多个分布式对手，是分布式的数据源数据流，攻防的组合招式是数据流的管道
```clojure
```
### 功夫中的双截棍等武器，是数据流管道的用的帮助工具
```clojure
```
### 咏春分手(小念头的分手在第二段，寻桥分手加了转马)，手像两个盾牌一样，攻击连消带打 ，来留去送 ，甩手直冲。。。而不是他打我，我后退马，只是防御 ，没有攻击的防御是没用的 => 分手训练，小念头和寻桥分手训练，一手标一伏，发力为一体的两手，而不是分裂的，但是分工不一样
```clojure
```
### 离开我中线，非中线向前，就可以出击 ，用黐手的打来提醒训练，发力错误，肘低发力 肩膀放松 归中三角形结构力 攻防才能奏效
```clojure
```
### 离开我就打他，叫甩手直冲
```clojure
```
### 来留去送 ，就像放风筝一样，顺着他的力 然后打他，如他向前较劲就拉打，他拉我就 我就撞打他
```clojure
```
### 生活中的中线原理和埋肘原理，守中用中: 归中  和 连消带打 111 用在朋友和高人身上一样奏效，父母身上，创造咏春拳的人 ，才是绝世大师，中线原理
```clojure
```

### 近邻分类(KNN)
```clojure
```
### 朴素贝叶斯分类
```clojure
```
### 决策树分类
```clojure
```
### 预测数值型数据: 广义回归方法
```clojure
```
### 神经网络和支持向量机
```clojure
```
### K均值聚类
```clojure
```

