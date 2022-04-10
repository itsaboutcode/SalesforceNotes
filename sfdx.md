# Salesforce CLI (SFDX)

## SFDX Command

#### Listing all the commands

```
sfdx commands
```

#### Update the SFDX 

``` 
sfdx update 
```

#### Getting Help on SFDX Commands

```
sfdx {command} --help
sfdx {command} -h

sfdx force:auth:web:login -h
```


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

#### Listing all connect orgs
```
sfdx force:org:list
```

# Reference

- [Salesforce CLI](https://developer.salesforce.com/tools/sfdxcli)
- [Salesforce CLI Setup Guide](https://developer.salesforce.com/docs/atlas.en-us.234.0.sfdx_setup.meta/sfdx_setup/sfdx_setup_intro.htm)
- [Salesforce DX Developer Guide](https://developer.salesforce.com/docs/atlas.en-us.sfdx_dev.meta/sfdx_dev/sfdx_dev_intro.htm)
- [Scratch Orgs](https://developer.salesforce.com/docs/atlas.en-us.sfdx_dev.meta/sfdx_dev/sfdx_dev_scratch_orgs.htm)
- [Trailhead | Build Apps Together with Package Development](https://trailhead.salesforce.com/en/content/learn/trails/sfdx_get_started)
