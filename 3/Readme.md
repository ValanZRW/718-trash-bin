Question 1
----------
loading the csv while selecting reasonable datatype automatically  
(https://stackoverflow.com/questions/44625888/why-the-types-are-all-string-while-load-csv-to-pyspark-dataframe)  

Question 2
----------

seaborn plot pack  
(https://www.geeksforgeeks.org/python-seaborn-pairplot-method/)

Question 3
----------
- transform the string into ordinal numbers  
(https://stackoverflow.com/questions/57641702/stringindexer-where-category-levels-passed-as-list)<br>
e.g. StringIndexerModel.from_labels(["a", "b", "c", "d", "e"], inputCol="A", outputCol="A_idx")

- pipeline foundation  
e.g. Pipeline(stages = [stage1, stage2, stage3])

        va = feature.VectorAssembler(inputCols=['bmi'], outputCol='features')  // This transforms a column/columns in to a input vector named features
        lr = regression.LinearRegression(featuresCol='features', labelCol='disease_progression')  // This applies the LR model.
        pipe = Pipeline(stages=[va, lr])  // This build a pipeline for future use.

    In this question, the stages is the StringIndexerModel above. So the final code may looks like

        stage1 = StringIndexerModel.from_labels(["a", "b", "c", "d", "e"], inputCol="A", outputCol="A_idx")
        stage2 = StringIndexerModel.from_labels(["a", "b", "c", "d", "e"], inputCol="B", outputCol="B_idx")
        stage3 = StringIndexerModel.from_labels(["a", "b", "c", "d", "e"], inputCol="C", outputCol="C_idx")
        pipe = Pipeline(stages = [stage1, stage2, stage3])

- how to apply the pipeline  

        pipe_model = pipe.fit(df) //returns the model which uses df as the input of the pipe
        res = pipe_model.transform(df) //returns the dataframe of inputing the df to the model

- remember drop useless columns and rename those ordinal columns

Question 4
----------

- two stages should be built. one is VectorAssembler, while the other is LR. Hence, a pipeline can be built then.

        va = feature.VectorAssembler(inputCols=[''], outputCol='features')  // This transforms a column/columns in to a input vector named features
        lr = regression.LinearRegression(featuresCol='features', labelCol='')  // This applies the LR model.
        pipe = Pipeline(stages=[va, lr]) 

- train and test split  
(http://spark.apache.org/docs/latest/api/python/pyspark.sql.html?highlight=randomsplit#pyspark.sql.DataFrame.randomSplit)

- construct an evaluator
(http://spark.apache.org/docs/latest/api/python/pyspark.ml.html?highlight=regressionevaluator#pyspark.ml.evaluation.RegressionEvaluator)

        evaluator = evaluation.RegressionEvaluator(predictionCol='prediction', labelCol='price', metricName='mse')

- evaluate the model 

        evaluator.evaluate(pipe.fit(train).transform(train))

Question 5
----------

(https://stackoverflow.com/questions/45420112/cross-validation-in-pyspark)

Question 6
----------

Question 7
----------

Question 8
----------

Extra credit
------------
