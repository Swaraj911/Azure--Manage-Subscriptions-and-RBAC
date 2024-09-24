# Azure--Manage-Subscriptions-and-RBAC
## Overview
This project demonstrates how to use permissions and scopes to control what actions identities can and cannot perform.
Also demonstrates how to make subscription management easier using management groups.

## Prerequisites
- An active Azure subscription
- Azure Portal access

## Steps to Manage Subscriptions and RBAC

### Step 1: Implement Management Groups
1. Sign in to the Azure portal- [https://portal.azure.com].
2. Search for and select [Microsoft Entra ID].
3. In the Manage blade, select Properties.
4. Review the Access management for Azure resources area. Ensure can manage access to all subscriptions and management
   groups in the tenant.
5. Search for and select [Management groups].
6. On the Management groups blade, click +Create.
7. Create management group with the following settings. Select Submit when you are done.
   SETTING:-
   a) Management group ID: az104-mg1(must be unique in the directory)
   b) Management group display name: az104-mg1
9. Refresh the management group page to ensure your displays. This may take a minute.

### Step 2: Review and assign a built-in Azure role
1. Select the az104-mg1 management group.
2. select the Access control (IAM) blade, and then the Roles tab.
3. Scroll through the built-in role definitions that are available. View a role to get detailed information about the
   Permissions, JSON, and Assignments. You will often use owner, contributor, and reader.
4. Select +Add, from the drop-down menu, select Add role assignment.
5. On the Add role assignment blade, search for and select the Virtual Machine Contributor. The Virtual machine
   contributor role lets you manage virtual machines, but not access their operating system or manage the virtual network
   and storage account they are connected to. This is a good role for the Help Desk. Select Next.
6. On the Members tab, Select Members.
   (Note: The next step assigns the role to the helpdesk group. If you do not have a Help Desk group, take a minute to 
    create it.)
7. Search for and select the [helpdesk] group. Click Select.
8. Click Review + assign twice to create the role assignment.
9. Continue on the Access control(IAM) blade. On the Role assignments tab, confirm the helpdesk group has the Virtual Machine
   Contributor role.

### Step 3: Create a custom RBAC role
1. Continue working on your management group. Navigate to the Access control(IAM) blade.
2. Select + Add, from the drop-down menu, select Add custom role.
3. On the Basics tab complete the configuration.
   SETTING:-
   a) Custom role name: Custom, Support, Request
   b) Description: A custom contributor role for support requests.
4. For Baseline permissions, select Clone a role. In the Role to clone drop-down menu, select Support Request Contributor.
   ![Screenshot 2024-09-24 205724](https://github.com/user-attachments/assets/e0eacd40-d21a-40ac-aea4-da6b6e5b80d0)
5. Select Next to move to the Permissions tab, and then select + Exclude permissions.
6. In the resource provider search field, enter [.Support] and select Microsoft.Support.
7. In the list of permissions, place a checkbox next to Other: Registers Support Resource Provider and then select Add. The
   role should be updated to include this permission as a NotAction.
8. On the Assignable scopes tab, ensure your management group is listed, then click Next.
9. Review the JSON for the Actions, NotActions, and AssignableScopes that are customized in the role.
10.Select Review + Create, and then select Create.
   (Note: At this point, you have created a custom role and assigned it to the management group.)

### Step 4: Monitor role assignments with the Activity Log
1. In the portal locate the az104-mg1 resource and select Activity log. The activity log provides insight into subscription-
   level events.
2. Review the activites for role assignments. The activity log can be filtered for specific operations.
   ![Screenshot 2024-09-24 212021](https://github.com/user-attachments/assets/05e92e29-f0d1-4ea5-bcc1-5e70e9669db8)

## Key takeaways
- Management groups are used to logically organize subscriptions.
- The built-in root management group includes all the management groups and subscriptions.
- Azure has many built-in roles. You can assign roles to control access to resources.
- You can create new roles or customize existing roles.
- Roles are defined in a JSON formatted file and include Actions, NotActions, and AssignableScopes.
- You can use the Activity Log to monitor role assignments.
