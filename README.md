# spotguide-zeppelin

Apache Zeppelin is a web-based notebook that enables data-driven interactive data analytics, providing built-in integration for Apache Spark and having about five different interpreters able to execute **Scala**, **Python**, **R** and **SQL** code on Spark. These interpreters are running remotely, managed by **RemoteInterpreterServer**.

This `spotguide` includes a Zeppelin Server integrated with Spark 2.3.2 running Scala and SQL code natively on Kubernetes. Python and R support is coming soon with Spark 2.4.

To run **RemoteInterpreterServer** Zeppelin uses the well known Spark tool, **spark-submit**. Spotguide starts up a Zeppelin Server with a preconfigured Spark interpreter to run Spark Driver and Executors pods on your Kubernetes cluster, by setting `spark.submit.deployMode` property to `cluster`. In Spark 2.3.2 dynamic allocation is not supported so you can specify the number of executors on Interpreter settings page: `spark.executor.instances`.

By default the `Spark` interpreter is configured `Per Note` with `isolated` scope, meaning there's a separate Spark Driver launched for each Zeppelin notebook / user.
Spark driver & executors pods names are prefixed with `spark.app.name` (zri) and the id of the interpreter group.
You can checkout by opening your clusters Kubernetes Dashboard from Pipeline UI.

Spark logs are saved to the bucket specified by you, however they are persisted only after `spark` interpreter has been stopped or restarted. You can restart your interpreter at Zeppelin Interpreter Settings page.
