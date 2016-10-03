# Spark AppVeyor Scripts

This repository has some scripts to launch a build against each Pull Reqeust on Windows.
It runs a build after checking out the given Pull Reqeust, creating a branch (named UUID),
updating `appveyor.yml` and then pushing the branch, printing a pretty string for the
information of the build launched.

### Precondition

The forked repository should be authroized and registered in AppVeyor CI tool. Please refer
[this documentation](https://github.com/apache/spark/blob/master/dev/appveyor-guide.md#setting-up-appveyor) to set up your repository with AppVeyor CI.

### Quick Start

- If this is not initiated once, `./dev/init [REPO_URL]` script should be run first,
  where `REPO_URL` is the url of your repositry forked from Apache Spark. For example,

  ```bash
  ./dev/init https://github.com/spark-test/spark.git
  ```

- Then, you can trigger the build with `./launch-build [PR_NUM] [COMPONENT] [SUITE]`
  where `PR_NUM` is the Pull Reqeust number which appears in at the end of the Pull Request
  title, `COMPONENT` is the component name in Apache Spark which the Pull Reqeust tries to fix
  and then `SUITE` is the test class name to run. For example,

  - Running SparkR tests (for `SparkR`, `SUITE` is ignored and run all tests)

    ```bash
    ./launch-build 15253 SparkR
    ```

  - Running Spark tests, `org.apache.spark.sql.sources.CreateTableAsSelectSuite` in SQL component

    ```
    ./launch-build 14242 SQL org.apache.spark.sql.sources.CreateTableAsSelectSuite
    ```

  - Running Spark tests, `org.apache.spark.deploy.SparkSubmitSuite` in CORE component

    ```
    ./launch-build 14242 CORE org.apache.spark.deploy.SparkSubmitSuite
    ```

  After running this script, it will print a pretty string to copy and paste to GitHub command.
  For example,

  ```
  Build started: [CORE] `org.apache.spark.storage.DiskStoreSuite` [![PR-15320](https://ci.appveyor.com/api/projects/status/github/spark-test/spark?branch=097F2F95-4748-4435-967F-98980DB2112E&svg=true)](https://ci.appveyor.com/project/spark-test/spark/branch/097F2F95-4748-4435-967F-98980DB2112E)
  ```

  which shows up as below:

  > Build started: [CORE] `org.apache.spark.storage.DiskStoreSuite` [![PR-15320](https://ci.appveyor.com/api/projects/status/github/spark-test/spark?branch=097F2F95-4748-4435-967F-98980DB2112E&svg=true)](https://ci.appveyor.com/project/spark-test/spark/branch/097F2F95-4748-4435-967F-98980DB2112E)

**NOTE: Currently, PySpark tests and running individual SparkR tests are not supports.**
