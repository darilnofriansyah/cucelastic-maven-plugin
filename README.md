# Real-time reporting of cucumber tests to Elastic Search

## Elastic Search and Kibana for Cucumber Reports

This is a revamp of the cucelastic plugin. The revamp added:
1. **Error Summary** - I added error summary to specify which error that happens in a certain scenario within certain project. This feature is dedicated to help QA Engineers documentation for error that happens within their project.
2. **Error Category** - I added categorization based on the tools that QA Engineers have within their project. They need to add them manually through the plugin in **CategoryEnum.java** files so that the plugins can record what tools they have and categorize the error based on the tools they have. For example, if you use **Selenium**, then you can add "selenium" to the category enum for UI errors.

To use the plugin, you need to add this plugin to your local computer by:
````
git clone https://github.com/darilnofriansyah/cucelastic-maven-plugin.git
````
Then, install the plugin to your computer by:
````
mvn clean install
````
The plugin is now inside your local computer.
To begin using the plugin for your cucumber project, you can add this line to the **pom.xml** inside your cucumber project:
````
<plugin>
    <groupId>com.araj.cucumber.elasticsearch</groupId>
    <artifactId>cucelastic-maven-plugin</artifactId>
    <version>1.0</version>
    <executions>
        <execution>
            <id>cucumber-elastic-search</id>
            <phase>post-integration-test</phase>
            <goals>
                <goal>load</goal>
            </goals>
        </execution>
    </executions>
    <configuration>
        <skip>false</skip>
        <sourceJsonReportDirectory>${project.build.directory}/destination</sourceJsonReportDirectory>
        <sendFeatureSummaryToElasticSearch>false</sendFeatureSummaryToElasticSearch>
        <sendScenarioSummaryToElasticSearch>false</sendScenarioSummaryToElasticSearch>
        <sendStepSummaryToElasticSearch>false</sendStepSummaryToElasticSearch>
        <sendTagSummaryToElasticSearch>false</sendTagSummaryToElasticSearch>
        <sendErrorSummaryToElasticSearch>true</sendErrorSummaryToElasticSearch>
        <sendCategoryToElastichSearch>true</sendCategoryToElastichSearch>
        <elasticSearchHostName>localhost:9200</elasticSearchHostName>
        <featureSummaryIndex/>
        <scenarioSummaryIndex/>
        <stepsSummaryIndex/>
        <tagsSummaryIndex/>
        <errorSummaryIndex/>
        <categoryIndex/>
        <featureSummaryDocumentType/>
        <scenarioSummaryDocumentType/>
        <stepsSummaryDocumentType/>
        <tagSummaryDocumentType/>
        <errorSummaryDocumentType>_doc</errorSummaryDocumentType>
        <categoryDocumentType/>
        <projectName>${project.artifactId}</projectName>
    </configuration>
</plugin>
````

You can modify the configuration as you like for your own personal purpose.
That's it. You can use the plugin now and retrieve data to be sent to elasticsearch.

