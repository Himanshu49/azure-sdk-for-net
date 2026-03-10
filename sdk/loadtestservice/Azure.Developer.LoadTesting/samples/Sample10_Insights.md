# Insights

To use these samples, you'll first need to set up resources. See [getting started](https://github.com/Azure/azure-sdk-for-net/blob/main/sdk/loadtestservice/Azure.Developer.LoadTesting/README.md#getting-started) for details.

Insights provide analysis and recommendations for your load test runs. You can generate insights for a test run and retrieve them to understand performance patterns.

## Create LoadTestRunClient
```C# Snippet:Azure_Developer_LoadTesting_CreateRunClient
// The data-plane endpoint is obtained from Control Plane APIs with "https://"
// To obtain endpoint please follow: https://github.com/Azure/azure-sdk-for-net/tree/main/sdk/loadtestservice/Azure.Developer.LoadTesting#data-plane-endpoint
Uri endpointUrl = new Uri("https://" + <your resource URI obtained from steps above>);
TokenCredential credential = new DefaultAzureCredential();

// creating LoadTesting Run Client
LoadTestRunClient loadTestRunClient = new LoadTestRunClient(endpointUrl, credential);
```

## Generate an Insight

Create an insight for a specific test run.

```C# Snippet:Azure_Developer_LoadTesting_GenerateInsight
string testRunId = "my-test-run-id";
string insightId = "my-insight-id";

var data = new
{
    displayName = "My Test Run Insight",
    description = "Insight generated for test run analysis",
};

try
{
    Response response = loadTestRunClient.CreateOrUpdateInsight(testRunId, insightId, RequestContent.Create(data));
    Console.WriteLine(response.Content.ToString());
}
catch (Exception ex)
{
    Console.WriteLine(ex.Message);
}
```

## Get an Insight

Retrieve a specific insight by its Id.

```C# Snippet:Azure_Developer_LoadTesting_GetInsight
try
{
    Response getResponse = loadTestRunClient.GetInsight(testRunId, insightId, context: null);
    Console.WriteLine(getResponse.Content.ToString());
}
catch (Exception ex)
{
    Console.WriteLine(ex.Message);
}
```