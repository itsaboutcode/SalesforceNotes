# [Automation: Workflow Rules and Approval Processes](https://www.youtube.com/playlist?list=PL8O9iwxpgTOJF4URmi0xv-InXvyIjSUB7)

## Automation Tools in Salesforce

1. Workflow Rules
2. Process Builder
3. Flow

Workflow Rules and Process Builder will [expire](https://admin.salesforce.com/blog/2021/go-with-the-flow-whats-happening-with-workflow-rules-and-process-builder?_ga=2.10245429.1298397712.1655204672-1608855082.1652624987) in future. So make sure you are using Salesforce Flow.

## Why you need automation

Each business is unique and may have some tasks which must be done when a certain action took place in your org. For example, when you close a deal, you should generate an email, which congratulate the account etc and it must be done. Since it's required step and require little to no input from user, it's ideal case for automation.

## Flow

- Flows can be better described as visual coding—they’re declarative, but they require that you understand some programming concepts like variables and how logic works.
- Flows are useful for two major use cases.
- Salesforce Flow are **two** point-and-click automation tools: **Flow Builder**, which lets you build flows, and **Process Builder**, which lets you edit existing processes.

- **Salesforce Flow** is the name of the **product**.
- **Flow Builder and Process Builder** are the names of the **tools**.
- Use Flow Builder to **make flows**; use Process Builder to refine existing **processes**.

### Behind-the-Scenes Automation

When you wanted a process to run when a record changes, you have your pick of solutions.

- Build an autolaunched flow that specifies a record trigger in **Flow Builder**.
- Build an **Apex trigger** with Apex code.

### Guided Visual Experiences

If your business process requires **input from a user**, you can use a:

- Screen flow
- Lightning component


### Terminology

- **Salesforce Flow** — the product that encompasses building, managing, and running flows and processes.
- **Flow Builder** — a point-and-click tool for building flows. 
- **Flow** — the part of Salesforce Flow that automates a business process by collecting data and doing something in your Salesforce org or an external system.

### Sub-topics

- Given a scenario, identify appropiate automation solution based on the capablities of the tool.
- Describe capabilities and use cases for **Flow**.
- Describe capabilities and use cases for the **Approval Process**.

### Intro to Flow Builder

- It's a latest and third automation tool for Salesforce.
- It's the most power and have most options. 
- It's suppose to replace **Workflow Rules and Process Builder.**
- You can access it from **Setup->Process Automation->Flows.**

#### Flow Interview
- A flow interview is a running instance of a flow.

#### Flow Building Blocks

- Flow have 3 building blocks.

1. Elements

- Elements perform logical actions e.g; assignment, decisions, or loops.
- There are also data elements that will query the database or commit record changes.


2. Connectors

- Arrows which connect all of our different elements and determine which element is going to lead to which.
- Autolayout allow you connect elements together automatically.


3. Resources

- Individual **variables** of data that can be used inside the flow e.g; strings, numbers, records, formulas, collection of numbers of reports.

### Process Builder

Process Builder is a point-and-click tool that lets you easily automate **if/then** business processes and see a graphical representation of your process as you build.

- It's 2nd automation tool in Salesforce. 
- It was build after **Workflow Rules**.

#### Components of a Process

Every process consists of 

- A **trigger**. 
- At least one **criteria** node.
- At least one **action**.

You can configure **immediate actions or schedule actions** to be executed at a **specific time**.


##### Trigger: Identify When the Process Should Run

##### Criteria: Determine Whether or Not to Execute Actions

##### Actions: What the Process Should Do


- Actions of Process Builder are

1. Create a record
2. Update records
3. Send email
4. Post to Chatter
5. Send custom notifications
6. Use an action
7. Submit for approval
8. Launch a flow
9. Launch a process
10. Call Apex
11. Manage Quip documents
12. Cross object updates for related records.

There is one thing which workflow can do, but process build can't. Workflow can send outbound messages.

- Key feature of Process Builder are

1. You can use it to submit record for approval.
2. Highly visual compared to workflow rules.
3. Allow controll over the order of action it fires.

#### Process Build Considerations

- Allows for 50 versions of a process total. Only one can be active a time.
- Processes can be launched from changes on the record, when invoked by another process, or when a platform event occurs.
- Outbound messages are not supported, but you can use the call apex action to achive this.
- Actions are executed in the order in which they appear in the process.
- Easily reorder critera using drag and drop.
- Reuse names when creating a new process version.

#### Scheduled Actions in Process Builder

- A process can have multiple scheduled actions per criteria node
- Scheduled action cannot be used when using the 'Evaluate Next Criteria' option.
- Admins receive an email alert if a suer who starts a process become inactive and scheduled actions fail.

### Ways To Call A Flow

### Workflow Rules




### Debugging Flows

### Approving an Approval Request

### Approval Process

### Flows Running in Context

### Flow Elements Tab

### Flow Manager Tab



# Reference

- https://trailhead.salesforce.com/live/videos/a2r3k000001WFTX/preparing-for-your-admin-certification-automation-workflow-rules-and-approval-processes/?lang=en
- [Projec: Build a Discount Approval Process](https://trailhead.salesforce.com/content/learn/projects/build-a-discount-approval-process)
- [Trail: Build Flows with Flow Builder](https://trailhead.salesforce.com/en/content/learn/trails/build-flows-with-flow-builder)
- [Trail: Automate Your Business Processes with Salesforce Flow](https://trailhead.salesforce.com/en/content/learn/trails/automate_business_processes)
- [Module: Flow Concepts: Quick Look](https://trailhead.salesforce.com/en/content/learn/modules/flow-concepts-quick-look)
- [Guide: Automate Your Business Processes](https://help.salesforce.com/s/articleView?id=sf.extend_click_process.htm&type=5)

