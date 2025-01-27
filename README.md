# oaltg: OpenAPI AWS Lambda Terraform Generator

## What
Embed OpenAPI operation metadata in your API Gateway resources defined in Terraform HCL and generate an OpenAPI spec.

## Why
Because there's no router involved in Golang Lambda handlers - it lives in your IaC.

```hcl
resource "aws_api_gateway_method" "get_pets" {
  # @openapi
  # summary: List all pets
  # parameters:
  #   - name: limit
  #     in: query
  #     schema:
  #       type: integer
  #       format: int32
  # responses:
  #   '200':
  #     description: A list of pets
  #     content:
  #       application/json:
  #         schema:
  #           type: array
  #           items:
  #             $ref: '#/components/schemas/Pet'
  rest_api_id   = aws_api_gateway_rest_api.example.id
  resource_id   = aws_api_gateway_resource.pets.id
  http_method   = "GET"
  authorization = "NONE"
}
```

`$ oaltg generate spec.yaml`
