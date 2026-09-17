Configure Privileged Identity Management
Alec I. Gillis September 2026

Overview
Privileged Identity Management (PIM) is a Microsoft Entra ID service that enables just-in-time (JIT) privileged access to Azure and Microsoft Entra roles. Instead of granting permanent admin access — which creates a persistent attack surface — PIM requires users to request and activate elevated access for a limited time window, with optional approval and justification requirements.
This lab will enumerate the process of configuring PIM for the Conditional Access Administrator role, enforcing an approval-based activation workflow, and validating that elevated access works as expected.

Lab Environment
This lab runs on a M365 Tenant with no special configuration needed.
The M365 Tenant provided for this lab has pre-established authentication and user data. Nonetheless, the process for configuring PIM should apply uniformly with any organization using M365/Entra ID for Identity Management.

Lab Tasks
This lab uses two accounts: a Global Administrator account, and a sample User account. With these accounts, we will accomplish the following:
1.
Assign the Conditional Access Administrator role as a PIM-eligible role assignment
2.
Configure activation settings including a time limit, justification requirement, and approver
3.
Request and approve a role activation using two separate accounts
4.
Verify that the activated role grants the expected access
5.
Deactivate the role to close the just-in-time access window
Lab Tasks
Assign a PIM-eligible role
In this section, you assign the Conditional Access Administrator role to Adele Vance as an eligible
assignment. An eligible assignment means the user does not hold the role permanently — they must
request and activate it each time they need it.
1. Sign in to the Microsoft Entra Admin Center at https://entra.microsoft.com as MOD
Administrator using Username and password.
2. In the left navigation, expand ID Governance and select Privileged Identity Management.
3. Under Manage, select Microsoft Entra roles.
4. Select Roles, then select Conditional Access Administrator, then + Add Assignment
5. On the + Add assignments page, configure the following:
Setting Value
Select role Conditional Access Administrator
Select members Adele Vance
Assignment type Eligible (after using the Next button)
6. Select Next, then select Assign to save the assignment.
7. On the Assignments page, confirm that Adele Vance appears under the Eligible assignments
tab with the role of Conditional Access Administrator.
Note: An eligible assignment does not grant access — it only enables the user to request activation. No
access is active at this point. If you receive an error Role Assignment Failed, wait several minutes and
try again.
Configure activation settings
PIM role settings control how the activation process works: how long the activation lasts, whether a
justification is required, and whether an approver must approve each request. You will now configure
the Conditional Access Administrator role settings.
8. In Privileged Identity Management > Microsoft Entra roles, select Settings.
9. Find and select Conditional Access Administrator from the role list.
10. Select Edit to open the role settings.
11. On the Activation tab, configure the following settings:
Setting Value
Activation maximum
duration
1 hour
On activation, require Justification
Require approval to activate Enabled
Other settings Leave at default value
12. Under Select approvers, select + Select members.
13. Search for and select MOD Administrator, then choose Select.
Note: If the approver pane is blank, close it and leave No approver selected. When no specific
approver is selected, Privileged Role Administrators and Global Administrators become the default
approvers. Because MOD Administrator is a Global Administrator, you can continue with the same
approval workflow.
14. Select Update to save the role settings.
15. Verify the role settings page now shows:
a. Maximum activation duration: 1 hour
b. Approval required: Yes
c. Approver: MOD Administrator, or the default Global Administrators if you used the
fallback
Request role activation
Now you will sign in as Adele Vance and submit a role activation request. This simulates a user who
needs temporary elevated access to perform a specific task.
16. Open a new InPrivate or Private browser window.
17. Navigate to the Entra admin center using https://entra.microsoft.com. Sign in to the Adele
Vance account using Username AdeleV@zzzzzzzzzz.OnMicrosoft.com and Password.
18. In the left navigation, expand ID Governance and select Privileged Identity Management.
19. Under Tasks, select My roles.
20. Select the Microsoft Entra roles tab.
21. Under Eligible assignments, find Conditional Access Administrator and select Activate.
22. On the Activate pane, configure the following:
Setting Value
Duration 1 hour
Justification Reviewing and updating Conditional Access
policies as part of a scheduled security review.
23. Select Activate.
You will see a confirmation that the request is pending approval. The role is not yet active — it requires
approval from MOD Administrator before access is granted.
24. Leave this browser window open — you will return to it after approving the request.
Approve the activation request
You will now switch back to the MOD Administrator browser window and approve the pending activation
request.
25. Return to your primary browser window (MOD Administrator is currently signed in).
26. Navigate to the Microsoft Entra Admin center.
27. In the left navigation, expand ID Governance and select Privileged Identity Management.
28. Under Tasks, select Approve requests.
29. Select the Microsoft Entra roles menu item.
30. Find the pending request from Adele Vance for the Conditional Access Administrator role.
31. Add a mark in the box next to the request, then select Approve.
Note: If the approval details pane is blank, refresh the Approve requests page once. Select the request again,
and then select Approve.
32. In the Justification field, enter: Approved for scheduled security review task.
33. Select Submit.
You should see an approval message pop-up.
34. You can now minimize this browser window.
Verify the activated role
Return to the Adele Vance browser window and verify that the role of activation succeeded and grants the
expected access.
35. In the Adele Vance browser window, refresh the page.
36. In Privileged Identity Management > My roles > Microsoft Entra roles, select the Active
assignments tab.
37. Confirm that Conditional Access Administrator appears with a status of Active and an expiration
time approximately 1 hour from now.
Test the activation in Conditional Access
38. Look at the menu on the left.
39. In the left navigation, find the Entra ID section and select Conditional Access.
40. Select + Create New policy to open the policy creation pane.
Note: If you can open the new policy pane, the role is active and granting the expected permissions. A user
without this role would see an error or the option would be unavailable.
41. Select X to close the policy pane without saving — creating a policy is not required for this
verification step.
Deactivate the role
Just-in-time access means access should be released as soon as the task is complete — not held until the time
window expires. You will now manually deactivate the Conditional Access Administrator role for Adele
Vance.
42. Return to the Adele Vance browser window (My roles show the currently signed-in user's
assignments, so deactivation must be done from Adele's window — not the MOD Administrator
window).
43. Navigate to Privileged Identity Management > My roles > Microsoft Entra roles > Active
assignments.
44. Find the Conditional Access Administrator assignment and select Deactivate.
45. In the confirmation dialog, select Deactivate again.
46. Confirm the role no longer appears under Active assignments and has returned to Eligible
assignments only.
The access window is now closed. If Adele needs to perform CA Admin tasks again, she must submit a new
activation request.
Summary
In this lab, you configured Privileged Identity Management to enforce just-in-time access to the Conditional
Access Administrator role. You assigned an eligible role to Adele Vance, configured activation settings with a
time limit, justification requirement, and named approver, then walked through the full activation and
approval workflow. You verified that the activated role granted the expected access and manually
deactivated the role to close the access window.
You have successfully completed this exercise.
Clean up
The lab environment is automatically reset at the end of the session. No manual resource deletion is
required.
If you want to clean up the PIM assignment before the session ends:
1. Sign in to the Entra Admin Center as your Global Administrator.
2. Navigate to Privileged Identity Management > Microsoft Entra roles > Assignments.
3. Find the Conditional Access Administrator eligible assignment for Adele Vance.
4. Select Remove and confirm.
