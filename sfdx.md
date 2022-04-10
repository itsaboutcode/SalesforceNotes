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

#### Listing all the orgs

List all orgs you’ve created or authenticated to.

```
sfdx force:org:list
```
##### Exaple Org listing

```
=== Orgs
     ALIAS     USERNAME              ORG ID              CONNECTED STATUS
───  ────────  ────────────────────  ──────────────────  ────────────────
(U)  adil1445  adil@adil.com         00D0o0000026uUtEAM  Connected

```

#### Opening an org

```
sfdx force:org:open // Open default org
sfdx force:org:open --targetusername Open
sfdx force:org:open -u DevHub
sfdx force:org:open -u FullSandbox
sfdx force:org:open -u MyScratchOrg
```

#### [Creating SFDX Project](https://developer.salesforce.com/docs/atlas.en-us.sfdx_cli_reference.meta/sfdx_cli_reference/cli_reference_force_project.htm)

This command creates a Salesforce DX project in the specified directory or the current working directory. The command creates the necessary configuration files and folders.

```
sfdx force:project:create -n {projectname}
sfdx force:project:create -n geolocation
```

#### [Deploy Changes](https://developer.salesforce.com/docs/atlas.en-us.sfdx_cli_reference.meta/sfdx_cli_reference/cli_reference_force_source.htm#cli_reference_force_source_deploy)

###### To deploy the source files in a directory in Developer Edition Org or a Trailhead Playground

```
$ sfdx force:source:deploy -p path/to/source
$ sfdx force:source:deploy -p .\force-app\
$ sfdx force:source:deploy --sourcepath .\force-app\
```

#### [Create Lightening App]()

#### [Create LWC]()

- First go to lwc folder `cd .\force-app\main\default\lwc\`
- To create a Lightning web component, pass **--type** lwc to the command. 
- If you don’t include a --type value, Salesforce CLI creates an Aura component by default.

```
$ sfdx force:lightning:component:create -n mycomponent --type lwc
```

#### Project Vs Bundle?

# Reference

- [Salesforce CLI](https://developer.salesforce.com/tools/sfdxcli)
- [Salesforce CLI Command Reference](https://developer.salesforce.com/docs/atlas.en-us.sfdx_cli_reference.meta/sfdx_cli_reference/cli_reference_top.htm)
- [Salesforce CLI Setup Guide](https://developer.salesforce.com/docs/atlas.en-us.234.0.sfdx_setup.meta/sfdx_setup/sfdx_setup_intro.htm)
- [Salesforce DX Developer Guide](https://developer.salesforce.com/docs/atlas.en-us.sfdx_dev.meta/sfdx_dev/sfdx_dev_intro.htm)
- [Scratch Orgs](https://developer.salesforce.com/docs/atlas.en-us.sfdx_dev.meta/sfdx_dev/sfdx_dev_scratch_orgs.htm)
- [Trailhead | Build Apps Together with Package Development](https://trailhead.salesforce.com/en/content/learn/trails/sfdx_get_started)
