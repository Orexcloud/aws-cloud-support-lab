## IAM review

Before starting the lab, I checked the IAM setup in the AWS account to see what was already there.

There is one IAM user, which is a member of an `admin` group. The group has the `AdministratorAccess` policy attached.

I also found an existing role called `DemoRoleForEC2`. The role trusts the EC2 service and has the `IAMReadOnlyAccess` policy attached.

The trust relationship allows EC2 to assume the role using `sts:AssumeRole`.

I didn't change or remove the existing role because it appears to be from previous AWS learning activity. I also decided not to use it for this lab because the permissions aren't needed for what I'm building.

### What I took from this

The main thing I wanted to refresh here was the difference between a role's trust policy and its permissions.

The trust policy controls who can assume the role. The permissions policy controls what the role can do once it has been assumed.

For the new environment, I'll create the permissions needed for the lab rather than reusing the old role.
