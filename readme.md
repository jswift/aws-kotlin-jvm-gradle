# Kotlin Gradle Serverless Template

This is a boilerplate template for [serverless](https://serverless.com/) using AWS, 
Kotlin, and Gradle.

## Requirements
 - Serverless 1.24 or higher
 - Gradle 4 and JDK8 
 
## Usage
```bash
# Create template
serverless create --template-url https://github.com/jswift/aws-kotlin-jvm-gradle \
    --path helloworld --name hello && cd helloworld

# Build and deploy the hello world function
gradle deploy
```

### Handlers
When developing _Handlers_ they should be updated to use the correct event, not the
default event as displayed in the template Handler. For example, a function that 
responds to a HTTP event would look like:

```kotlin
class Handler: RequestHandler<APIGatewayProxyRequestEvent, ApiGatewayResponse> {
    override fun handleRequest(event: APIGatewayProxyRequestEvent, context: Context): ApiGatewayResponse {
        // Do stuff
    }
}
```

### Response
Response objects extend the `Response` class and are converted to JSON. The simplest option
is to create a data class, as demonstrated in `HelloResponse`.

### AWS Java SDK
If you need to use the AWS Java SDK in your functions, you can use the Bill-of-Materials
(BOM) provided in the gradle file. When adding a library, such as _S3_, you just add
`compile 'com.amazonaws:aws-java-sdk-s3'` to the dependecies and it will ensure all
your libraries are at the correct version.
