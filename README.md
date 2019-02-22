# UserManagement

This is a lambda functions that includes 2 binaries from <https://github.com/rtucker-mozilla/nubis-bastionsshkey>
and <https://github.com/Versent/unicreds>

## Local testing

To test locally you will need to install the following node package

```bash
# npm install -g lambda-local
```

You will need to provide it with an event file (a sample is included in this
repo) and you can invoke the lambda function by running the following command

```bash
lambda-local -l index.js -h handler -e event.json
```

## Lambda Test Configuration

This is a no op test for the lambda function. It will print out a list of user
names in the CloudWatch logs. This will test the LDAP connection portion only.
If you remove the '-noop' flag it will also test the consul portion. Be sure to
replace `<ACCOUNT>` with the account name.

```json
{
  "command": "./nubis-user-management",
  "args": [
    "-execType=consul",
    "-useDynamo=true",
    "-region=us-west-2",
    "-arena=core",
    "-service=nubis",
    "-accountName=<ACCOUNT>",
    "-consulDomain=nubis.allizom.org",
    "-consulPort=80",
    "-key=nubis/core/user-sync/config",
    "-lambda=true",
    "-noop"
  ]
}
```
