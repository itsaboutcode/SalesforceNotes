# Salesforce CLI (SFDX)

#### Update the SFDX 

` sfdx update `


#### Authorize an org using the web login flow

```
USAGE
  $ sfdx auth:web:login [-i <string>] [-r <url>] [-d] [-s] [-a <string>] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

OPTIONS
  -a, --setalias=setalias                                                           set an alias for the authenticated org
  -d, --setdefaultdevhubusername                                                    set the authenticated org as the default dev hub org for scratch org creation
  -i, --clientid=clientid                                                           OAuth client ID (sometimes called the consumer key)
  -r, --instanceurl=instanceurl                                                     the login URL of the instance the org lives on
  -s, --setdefaultusername                                                          set the authenticated org as the default username that all commands run against
  --json                                                                            format output as json
  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)  [default: warn] logging level for this command invocation

DESCRIPTION
  If you specify an --instanceurl value, this value overrides the sfdcLoginUrl value in your sfdx-project.json file. To specify a My Domain URL, use the format MyDomainName.my.salesforce.com (not
  MyDomainName.lightning.force.com). To log in to a sandbox, set --instanceurl to https://MyDomainName--SandboxName.sandbox.my.salesforce.com.

ALIASES
  $ sfdx force:auth:web:login

EXAMPLES
  sfdx auth:web:login -a TestOrg1
  sfdx auth:web:login -i <OAuth client id>
  sfdx auth:web:login -r https://MyDomainName--SandboxName.sandbox.my.salesforce.com
```



# Reference

-[Salesforce CLI](https://developer.salesforce.com/tools/sfdxcli)
