Marlin
============

A distributed matrix operations library build on top of [Spark](http://spark.apache.org/). Now, the master branch is in version 0.3-SNAPSHOT.  

##Branches Notice
This branch(spark-marlin) built on a custom version Spark to get better performance for matrix operations, however this branch has not been published out. If you use the official version Spark, please refer to `master` branch.

##Prerequisites
As Marlin is built on top of Spark, you need to get the Spark installed first.  If you are not clear how to setup Spark, please refer to the guidelines [here](http://spark.apache.org/docs/latest/). Currently, this branch is developed on the APIs of Spark 2.0.x version. The optimized Spark Source code is [here]().

##Compile Marlin
We have offered a default `build.sbt` file, make sure you have installed [mvn] and you can just type `mvn package`	to get a package. 

##Run Marlin
We have already offered some examples in `edu.nju.pasalab.marlin.examples` to show how to use the APIs in the project. For example, if you want to run two large matrices multiplication, use spark-submit method, and type in command
 
	$./bin/spark-submit \
	 --class edu.nju.pasalab.marlin.examples.MatrixMultiply
	 --master <master-url> \
	 --executor-memory <memory> \
	 marlin_2.11-0.3-SNAPSHOT.jar \
	 <matrix A rows> <martrix A columns> \
	 <martrix B columns> <cores cross the cluster> <output path>

**Note:** Because the pre-built Spark-assembly jar doesn't have any files about netlib-java native compontent, which means you cannot use the native linear algebra library e.g BLAS to accelerate the computing, but have to use pure java to perform the small block matrix multiply in every worker. We have done some experiments and find it has a significant performance difference between the native BLAS computing and the pure java one, here you can find more info about the [performance comparison](https://github.com/PasaLab/marlin/wiki/Performance-comparison-on-matrices-multiply) and [how to load native library](https://github.com/PasaLab/marlin/wiki/How-to-load-native-linear-algebra-library).

**Note:** this example use `MTUtils.randomDenVecMatrix` to generate distributed random matrix in-memory without reading data from files.

**Note:** `<cores cross the cluster>` is the num of cores across the cluster you want to use. 

**Note:** `<output path>` is the file path you want to store the result matrix, this matrix is store in DenseVecMatrix Type 

##Martix Operations API in Marlin
Currently, we have finished some APIs, you can find documentation in this [page](https://github.com/PasaLab/marlin/wiki/Linear-Algebra-Cheat-Sheet).


##Algorithms and Performance Evaluation
The details of the matrix multiplication algorithm is [here](https://github.com/PasaLab/marlin/wiki/Matrix-multiply-algorithm).

###Performance Evaluation
We have done some performance evaluation of Marlin. It can be seen [here](https://github.com/PasaLab/marlin/wiki/Performance-comparison-on-matrices-multiply).

##Contact
gurongwalker at gmail dot com

myasuka at live dot com
