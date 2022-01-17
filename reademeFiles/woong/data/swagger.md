# OPENAPI& Swagger

- What is Swagger and OpenAPI?
- Why should you know about Swagger?
- OpenAPI Specification
- How to integrate OpenAPI and Swagger?

## Swagger

- Domain Specific Language

- Swagger Tool
> Swagger Specification 2.0 -> OpenAPI Specification 3.x.x
> Swagger Editor
> Swagger Codegen
> Swagger UI

## Why Swagger?
- How to model RESTful API? -> Swagger Editor
- How to document RESTful API? -> Swagger UI
- How to keep code and docs in sync? -> Swagger Codegen
- How to make API adoption easy? -> Swagger Codegen


### Code First API Development
👍 Faster API implementation
👍 Good Start point for existing projects
👎 API definition is scattered across the code
👎Focuses on the implementation not API design
- swagger-jsdoc-npm
- swagger-ui-express-npm

### Design First API Development
👍API definition is one source of truth
👍Early collaboration and feedback
👍Focus on API design yields better APIs
👎 Takes longer to develop and deliver APIs

- use Codegen(openapi-generator)
👎 No clear separation between generated code and hand-written handlers
👎 Cannot selectively use individual parts

- middleware(express-openapi-validator)
👍 Express middleware
👍 Validates request parameters and responses
👍includes costomisable router