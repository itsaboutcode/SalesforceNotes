- [Salesforce CLI (SFDX)](#salesforce-cli-sfdx)
  - [SFDX Command](#sfdx-command)
      - [Listing all the commands](#listing-all-the-commands)
      - [Update the SFDX](#update-the-sfdx)
      - [Getting Help on SFDX Commands](#getting-help-on-sfdx-commands)
      - [Authorize an org using the web login flow](#authorize-an-org-using-the-web-login-flow)
      - [Listing all the orgs](#listing-all-the-orgs)
        - [Exaple Org listing](#exaple-org-listing)
      - [Listing Org Aliases](#listing-org-aliases)
        - [Example Output](#example-output)
      - [Opening an org](#opening-an-org)
      - [Changing the default org for a Salesforce Project](#changing-the-default-org-for-a-salesforce-project)
        - [VSCode Steps](#vscode-steps)
      - [Creating SFDX Project](#creating-sfdx-project)
      - [Deploy Changes to Developer Edition Org or a Trailhead Playground](#deploy-changes-to-developer-edition-org-or-a-trailhead-playground)
          - [To deploy the source files in a directory in Developer Edition Org or a Trailhead Playground](#to-deploy-the-source-files-in-a-directory-in-developer-edition-org-or-a-trailhead-playground)
    - [Scratch Org](#scratch-org)
      - [Creating a Scratch Org](#creating-a-scratch-org)
      - [Creating a Scratch Org using VSCode](#creating-a-scratch-org-using-vscode)
        - [Step # 01](#step--01)
        - [Step # 02](#step--02)
        - [Step # 03](#step--03)
        - [Step # 04](#step--04)
      - [Deploy Changes to Scratch Org](#deploy-changes-to-scratch-org)
      - [Pull Source from the Scratch Org to Your Project](#pull-source-from-the-scratch-org-to-your-project)
      - [Create Lightening App](#create-lightening-app)
      - [Create LWC](#create-lwc)
        - [VSCode Steps](#vscode-steps-1)
      - [Project Vs Bundle?](#project-vs-bundle)
    - [Running Apex Anonymous Code](#running-apex-anonymous-code)
    - [Debugging Apex Code](#debugging-apex-code)
      - [Get Apex Debug Log](#get-apex-debug-log)
      - [Launch Apex Relay Debugger](#launch-apex-relay-debugger)
- [Reference](#reference)

# Salesforce CLI (SFDX)

## SFDX Command

#### Listing all the commands

```js
sfdx commands
```

#### Update the SFDX 

``` js
sfdx update 
```

#### Getting Help on SFDX Commands

```js
sfdx {command} --help
sfdx {command} -h

sfdx force:auth:web:login -h
```


#### Authorize an org using the web login flow

```js
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

```js
sfdx force:org:list
```
##### Exaple Org listing

```js
sfdx force:org:list
=== Orgs
    ALIAS         USERNAME              ORG ID      CONNECTED STATUS
    -----------   --------------------  --------    ----------------
    DD-ORG        jdoe@dd-204.com       00D...OEA   Connected
(D) devhuborg     jdoe@mydevhub.com     00D...MAC   Connected


    ALIAS      SCRATCH ORG NAME USERNAME                   ORG ID    EXPIRATION DATE
    ---------- ------------     -------------------------- --------- ----------
    my-scratch Your Company     test-wvkm5z113@example.com 00D...UAI 2017-06-13
(U) scratch208 Your Company     test-wvkm5z113@example.com 00D...UAY 2017-06-13
```

- The top section of the output lists the `non-scratch orgs` that you’ve authorized, including Dev Hub orgs, production orgs, and sandboxes. 
- A `(D)` on the left points to the `default Dev Hub org` username.

- The lower section lists the active scratch orgs that you’ve created.
- A (U) on the left points to the `default scratch org` username.

#### Listing Org Aliases

```js
sfdx alias:list
```

##### Example Output

```js
 Alias       Value
 ─────────── ─────────────────────────────────────────
 adil1535    a@hotmail.com
 jonmortgage j@w.co.uk.dev
```

#### Opening an org

```js
sfdx force:org:open // Open default org
sfdx force:org:open --targetusername Open
sfdx force:org:open -u DevHub
sfdx force:org:open -u FullSandbox
sfdx force:org:open -u MyScratchOrg
```

#### Changing the default org for a Salesforce Project

```js
sfdx force:config:set defaultusername=orgalias
sfdx config:set defaultusername=me@my.org defaultdevhubusername=me@myhub.org
sfdx config:set defaultdevhubusername=me@myhub.org
```

##### VSCode Steps

001

![default-org-1](https://user-images.githubusercontent.com/204423/164186916-8c26935e-e363-4587-8d80-ceb3462ace26.png)

002

![default-org-2](https://user-images.githubusercontent.com/204423/164187019-5ad071cd-9b5b-4e29-ae60-ba9d8d8cc49f.png)


#### [Creating SFDX Project](https://developer.salesforce.com/docs/atlas.en-us.sfdx_cli_reference.meta/sfdx_cli_reference/cli_reference_force_project.htm)

This command creates a Salesforce DX project in the specified directory or the current working directory. The command creates the necessary configuration files and folders.

```js
sfdx force:project:create -n {projectname}
sfdx force:project:create -n geolocation
```

#### [Deploy Changes to Developer Edition Org or a Trailhead Playground](https://developer.salesforce.com/docs/atlas.en-us.sfdx_cli_reference.meta/sfdx_cli_reference/cli_reference_force_source.htm#cli_reference_force_source_deploy)

###### To deploy the source files in a directory in Developer Edition Org or a Trailhead Playground

```js
$ sfdx force:source:deploy -p path/to/source
$ sfdx force:source:deploy -p .\force-app\
$ sfdx force:source:deploy --sourcepath .\force-app\
```

### Scratch Org

#### [Creating a Scratch Org](https://developer.salesforce.com/docs/atlas.en-us.sfdx_dev.meta/sfdx_dev/sfdx_dev_scratch_orgs_create.htm)

```js
sfdx force:org:create -f project-scratch-def.json -a MyScratchOrg --setdefaultusername
```

#### [Creating a Scratch Org using VSCode]()

##### Step # 01

![scratch-org](https://user-images.githubusercontent.com/204423/165761493-13379ede-676e-42e1-961d-024830ae8db7.png)


##### Step # 02


![scratch-org1](https://user-images.githubusercontent.com/204423/165761556-ebab30a5-f385-45de-9f5b-4b754f967fa3.png)


##### Step # 03

![scratch-org2](https://user-images.githubusercontent.com/204423/165761584-efce3d31-6e3e-4395-a4db-cdc51a85bc12.png)


##### Step # 04


![scratch-org3](https://user-images.githubusercontent.com/204423/165761613-08039b47-25de-456d-924d-58dcdfa2dea2.png)

#### [Deploy Changes to Scratch Org](https://developer.salesforce.com/docs/atlas.en-us.sfdx_dev.meta/sfdx_dev/sfdx_dev_push_md_to_scratch_org.htm)
```js
sfdx force:source:push --targetusername my-other-scratch-org
```

#### [Pull Source from the Scratch Org to Your Project](https://developer.salesforce.com/docs/atlas.en-us.sfdx_dev.meta/sfdx_dev/sfdx_dev_pull_md_from_scratch_org.htm)
```js
sfdx force:source:pull
```

#### [Create Lightening App]()

#### [Create LWC]()

- First go to lwc folder `cd .\force-app\main\default\lwc\`
- To create a Lightning web component, pass **--type** lwc to the command. 
- If you don’t include a --type value, Salesforce CLI creates an Aura component by default.

```
$ sfdx force:lightning:component:create -n mycomponent --type lwc
```

##### VSCode Steps

001

![vscode-create-lwc-1](https://user-images.githubusercontent.com/204423/164190897-b735ecaf-6624-42f3-8507-7b1b39ccd99a.png)

002

![vscode-create-lwc-2](https://user-images.githubusercontent.com/204423/164190974-fe8494a1-4622-4b44-897c-b24d69bcebe8.png)

003

![vscode-create-lwc-3](https://user-images.githubusercontent.com/204423/164191001-af4fb841-70a1-4a9a-8305-b004b5d5cf37.png)

#### Project Vs Bundle?


### Running Apex Anonymous Code

```js
sfdx force:apex:execute -f .\scripts\apex\hello.apex
```

In VSCode, you need to open the file and while on that file, select `Execute Anonymous Apex with Editor Content` option.

![vs-code-annonymous-code](https://user-images.githubusercontent.com/204423/163756136-21dffb8d-297f-4c50-929a-e874c560a1a3.png)

### Debugging Apex Code

#### Get Apex Debug Log

#### Launch Apex Relay Debugger



# Reference

- [Salesforce CLI](https://developer.salesforce.com/tools/sfdxcli)
- [Salesforce CLI Command Reference](https://developer.salesforce.com/docs/atlas.en-us.sfdx_cli_reference.meta/sfdx_cli_reference/cli_reference_top.htm)
- [Salesforce CLI Setup Guide](https://developer.salesforce.com/docs/atlas.en-us.234.0.sfdx_setup.meta/sfdx_setup/sfdx_setup_intro.htm)
- [Salesforce DX Developer Guide](https://developer.salesforce.com/docs/atlas.en-us.sfdx_dev.meta/sfdx_dev/sfdx_dev_intro.htm)
- [Scratch Orgs](https://developer.salesforce.com/docs/atlas.en-us.sfdx_dev.meta/sfdx_dev/sfdx_dev_scratch_orgs.htm)
- [Trailhead | Build Apps Together with Package Development](https://trailhead.salesforce.com/en/content/learn/trails/sfdx_get_started)
