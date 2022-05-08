- [Object Manager and Lightning App Builder: 20%](#object-manager-and-lightning-app-builder-20)
  - [Standard Objects](#standard-objects)
  - [Master-Detail Relationship](#master-detail-relationship)
  - [Roll-Up Summary Fields](#roll-up-summary-fields)
  - [Lookup Relationships](#lookup-relationships)
  - [Junction Relationship Object](#junction-relationship-object)
  - [Customization Relationship](#customization-relationship)
  - [Accounts and Contacts Relationship](#accounts-and-contacts-relationship)
  - [Changing and Deleting Fields](#changing-and-deleting-fields)
  - [Required Fields](#required-fields)
  - [Picklists](#picklists)
  - [Validation Rules](#validation-rules)
  - [Cross Object Formula](#cross-object-formula)
  - [Page Layouts and Field Level Security](#page-layouts-and-field-level-security)
  - [List Views and Search Layouts](#list-views-and-search-layouts)
  - [Lightning App Builder](#lightning-app-builder)
  - [Page Layout Assignments](#page-layout-assignments)
  - [Record Types](#record-types)
  - [Assignment Rules](#assignment-rules)
  - [Business Processes](#business-processes)
  - [Queues](#queues)
- [References](#references)

# [Object Manager and Lightning App Builder: 20%](https://www.youtube.com/playlist?list=PL8O9iwxpgTOIX5bsk7Lg5HNIPfunN5hdQ)

This topic has 3 sub-topics

1. Describe the standard `object architecture` and `relationship model.` It includes topics e.g.; Standard Objects, Parent-Child Relationship, Master-Detail Relationship, Lookup Relationship, Junction Objects and Relationship, and Record Types.

2. Create, delete and customize `fields` and `page layouts` on standard and custom objects and know the implications of deleting fields. It's all about `fields` and `page layouts`.

3. Assign page layout, record types, and business processes based on any given scenario for custom and standard objects.

## Standard Objects

Common Standard Object includes

| Object      | Description                                                                                      |
| :---------- | :----------------------------------------------------------------------------------------------- |
| Account     | Has 1:N relationship with cases and opportunities. Products and Campaigns are not related to it. |
| Contact     |                                                                                                  |
| Lead        |                                                                                                  |
| Opportunity |                                                                                                  |
| Case        | Customer Feedback, inquiry, or complaint.                                                        |
| Campaign    | Aimed at Campaign Members                                                                        |
| Products    | Related to opportunities                                                                         |
| Solution    | A regularly occurring customer problem that has the solution                                     |
| Work Order  | Tracks the different tasks that need to be taken out on a product                                |


## Master-Detail Relationship

- In this relationship, if you delete the master record, it automatically deletes the associated detail records.
  
- You can't give a new master to a detailed record.- There is no `owner field` in the detail record, instead, it's shared from the master record because the owner of the master record also owns the detailed record.

- Detailed records can't have `Sharing Rules, Manual Sharing, and Queues`, because these require an owner field, which detail records don't have.
  
- Detailed records inherit the `Sharing and security` settings of the master record.
  
- Master relationship field is required on all detailed page layouts (Permanent lookup field).- A custom object can have up to 2 master-detail relationships.

## Roll-Up Summary Fields

- These `fields` are only allowed on master records in a master-detailed relationship. Example fields includes
  
1. Count: count the number of related detail records for any given master record.

2. Sum: Accumulates different fields in the detailed records to be displayed on master record page.

## Lookup Relationships

Features of Lookup Relationship include

1. Loosely coupled
2. No roll-up summary fields.
3. Don't share security settings.
4. When you try to change the lookup relationship to the master-detail relationship, make sure every detailed object has a lookup field for the master object.
5. We can also create a `dependent lookup` field, a lookup field with a `filter` => You can only lookup objects or related records which satisfy the `filter` condition. 

- You always create a field on the N side of the 1:N relationship e.g.; 1 Provider can have N patients.
- On the 1 side, the related list is maintained.

## Junction Relationship Object

- This object is created to be used in a many-to-many relationship.
- This object will have `2 master-detail` relationships.

## Customization Relationship

## Accounts and Contacts Relationship

## Changing and Deleting Fields

## Required Fields

## Picklists

## Validation Rules

## Cross Object Formula

## Page Layouts and Field Level Security

## List Views and Search Layouts

## Lightning App Builder

## Page Layout Assignments

## [Record Types](https://www.youtube.com/watch?v=ZsFe0kohDRA)

- It's used to show different versions of one particular object.
  
- There can be multiple reasons to do it. e.g.; For different users, you don't want to show all the fields, or maybe different users needed to see different fields of the same object.
  
- Real-life examples include, you may be recording student library, accounts and courses information. For an accountant, library information maybe not useful.
  
- Another example can be, in a hospital, you can refer a patient and get a referral of a patient. When you are getting referral, the referral number field should be editable because you will be entering the value you got. In-case you are creating referral for a patient, it should be autogenerated and noneditable.

- when you use record type, you achieve the following 3 main things.

1. Show Different page layouts.
2. Show different picklist values.
3. Show different business processes.

## Assignment Rules

## Business Processes

## Queues



# References

- [Extend Salesforce with Clicks, Not Code](https://help.salesforce.com/s/articleView?id=sf.extend_click_intro.htm&type=5)
- [Trailhead | Admin Trail Mix](https://trailhead.salesforce.com/en/users/strailhead/trailmixes/prepare-for-your-salesforce-administrator-credential)
- [Trailhead | Admin Trail Basic Mix](https://trailhead.salesforce.com/en/content/learn/trails/force_com_admin_beginner)
- [Trailhead | Admin Trail Intermediate Mix](https://trailhead.salesforce.com/en/content/learn/trails/force_com_admin_intermediate)
- [Trailhead | Admin Trail Advance Mix](https://trailhead.salesforce.com/en/content/learn/trails/force_com_admin_advanced)
- [Salesforce Hulk | Salesforce Administrator and App Builder](https://www.youtube.com/playlist?list=PLWgzSrReOBh4P7kQyCJVH7mdmCWw0HXfi)
- [Tutorials Point | Salesforce](https://www.youtube.com/watch?v=BA-407HF_fM&list=PLWPirh4EWFpH2LYVIrfmA1RTredCySwP_)
- [Salesforce | Who see what](https://www.youtube.com/playlist?list=PLnobS_RgN7JZxK1wjUvQ84jMFqRZoJXbD)

