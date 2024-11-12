# AWS CLI Setup

To connect to the AWS account it is necessary to have a user in the console. Usually the one using to login can be taken. The connection needs a `key_id` and `access_key`.
### Creating a key
To create an Access Key you have to have a user for which the key should be created. In the console use the following command:
```bash
aws iam create-access-key --user-name <value>
```
`<value>` the name of the user the key will be created for

The Output of the command should look like this:
```JSON
{
    "AccessKey": {
        "UserName": "kk_labs_user_352199",
        "AccessKeyId": "ACCESSKEYID",
        "Status": "Active",
        "SecretAccessKey": "SUPERSECRETACCESSKEY",
        "CreateDate": "2024-08-22T22:22:12+00:00"
    }
}
```

### Adding a key to your local AWS CLI
To add the key to your local AWS CLI you can run the following command:
```bash
aws configure --profile <profile-name>
```
`<profile-name>` a string chosen to identify the created profile

The command will the promt your for the Access Key ID and the Secret Access Key which can be taken from the output of the previous command

### Using the profile
To use the previously created profile you have to append the following parameters to all your aws commands:
```bash
--profile <profile-name>
```
`<profile-name>` string chosen as identifier when creating the profile

### Manual changes
The created/used profile will be saved in `~/.aws/creadetials` where the key also can be added manually using the following syntax:
```
[<profile-name>]
aws_access_key_id = ACCESSKEYID
aws_secret_access_key = SUPERSECRETACCESSKEY
```
Changing the `<profile-name>` to `default`will make this key used by default and therefore allow you to omit the appending of the `--profile <profile-name>
