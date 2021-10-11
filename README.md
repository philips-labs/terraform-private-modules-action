# Terraform Private Modules Action

This is a composite GitHub action that allows you to use private terraform modules that are stored in GitHub repos.

It does this by using a git alias for your internal organisation that includes a github token.

This action should be used before any terraform commands. It gives access to any repos that the token supplied has action.

It is important to note that this allows access to any tool using Git and is not limited to terraform.

## Inputs

| Name  | Description                                           | Required |
| ----- | ----------------------------------------------------- | -------- |
| org   | The org where the private modules are stored.         | true     |
| token | The token that grants access to the repos in the org. | true     |

## Outputs

None.

## Example

```yaml
jobs:
  terraform:
    name: Terraform
    container: hashicorp/terraform
    steps:
      - uses: actions/checkout@v1

      - id: private-modules
        uses: philips-labs/terraform-private-modules-action@v1
        with:
          org: philips-internal
          token: ${{ secrets.MY_TOKEN }}

      - id: init
        run: terraform init
```
