Create a ECR repo and get the arn id
![Screenshot from 2023-01-07 14-07-20](https://user-images.githubusercontent.com/70542481/211141776-68d357a5-7814-40b8-b457-54e15b36b7c8.png)

To get the arn id of any ECR registry:
```arn_id
arn:aws:ecr:ap-south-1:117276297260:repository/<registry name>
```
Generate a IAM policy for private registry : `github-ecr-action-iam-policy.json`
```iam_policy
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowPullPush",
            "Effect": "Allow",
            "Action": [
                "ecr:GetDownloadUrlForLayer",
                "ecr:BatchGetImage",
                "ecr:CompleteLayerUpload",
                "ecr:UploadLayerPart",
                "ecr:InitiateLayerUpload",
                "ecr:BatchCheckLayerAvailability",
                "ecr:PutImage"
            ],
            "Resource": "arn:aws:ecr:ap-south-1:117276297260:repository/github-ecr-action"
        },
        {
            "Sid": "AuthToken",
            "Effect": "Allow",
            "Action": "ecr:GetAuthorizationToken",
            "Resource": "*"
        }
    ]
}
```
Create IAM Users for Access and Secret keys
![Screenshot from 2023-01-07 14-21-38](https://user-images.githubusercontent.com/70542481/211142323-de6b2870-41c7-453a-a667-3da3cd711c60.png)

Attact the IAM policy to IAM user
![Screenshot from 2023-01-07 14-22-51](https://user-images.githubusercontent.com/70542481/211142374-dbf53141-e2c3-4fb8-8ff2-b8b343552d53.png)
Get the cred, we need to put this github secrets
![Screenshot from 2023-01-07 14-24-34](https://user-images.githubusercontent.com/70542481/211142460-c3ac7a0b-6b93-4ff9-a2c6-cd7126de81a9.png)
</br> </br>
![Screenshot from 2023-01-07 14-27-59](https://user-images.githubusercontent.com/70542481/211142531-362d7216-ab6f-4e8c-a6df-e3317b770f95.png)

What is AWS_ROLE_TO_ASSUME ? </br>
> In this example, the secret AWS_ROLE_TO_ASSUME contains a string like arn:aws:iam::123456789100:role/my-github-actions-role. To assume a role in the same account as the static credentials, you can simply specify the role name, like role-to-assume: my-github-actions-role

Now we need to create Role. And we have to put that Role ARN inside `AWS_ROLE_TO_ASSUME` github secret
![image](https://user-images.githubusercontent.com/70542481/211142894-f1b696f4-5586-4f1c-b5cc-9168dec758cc.png)
than select the IAM policy
![image](https://user-images.githubusercontent.com/70542481/211142958-59b0dab6-545c-448f-b452-47c2c13dab47.png)
Now click on create Role
![image](https://user-images.githubusercontent.com/70542481/211143056-fd18f0e8-e4ff-4d48-b459-824bd41839ee.png)


