# IAM Security Review

## Existing AWS Environment

Before creating new infrastructure, I reviewed the existing IAM configuration in the AWS account.

### Existing IAM User

The account contains one IAM user. The user receives permissions through an administrator group with the `AdministratorAccess` managed policy.

### Existing EC2 Role

An existing IAM role named `DemoRoleForEC2` was identified.

**Trusted entity:** Amazon EC2

**Attached permission policy:** `IAMReadOnlyAccess`

### Trust Relationship

The role's trust policy allows the EC2 service to assume the role using `sts:AssumeRole`.

### Assessment

The role appears to have been created for previous AWS learning activities. Its permissions provide read-only access to IAM and are not required for the current cloud support lab.

The role was therefore reviewed but not modified or reused.

## Key Learning

IAM roles have two important components:

* **Trust policy:** defines who or what can assume the role.
* **Permissions policy:** defines what the role is allowed to do after it is assumed.

For the new lab environment, a separate role will be created with permissions appropriate to the workload and following the principle of least privilege.
