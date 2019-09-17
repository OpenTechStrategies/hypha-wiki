Below is are the projects objectives by time first and then by theme.

# By time
## Horizon 1
**Approx. next month**

See progress by reviewing [priority tickets](https://github.com/OpenTechFund/opentech.fund/labels/priority) for the current milestone ([2019-Q3](https://github.com/OpenTechFund/opentech.fund/milestone/2)) and/or todo list on the [main project board](https://github.com/OpenTechFund/opentech.fund/projects/2). 

### Dev goals
_From priority tickets within the current milestone ([2019-Q3 +priority](https://github.com/OpenTechFund/opentech.fund/issues?page=2&q=is%3Aopen+is%3Aissue+label%3Apriority+milestone%3A2019-Q3&utf8=%E2%9C%93))_

September

Dev Features
* Side-by-Side View
* Reminder function to applicants and staff reviewers to track and manage deadlines 
* Auto populate decision text into determination responses
* Word/Character Limits 
* Email text and correspondence
* Connect submissions that applied to other OTF funds within WebApp
* Usability/UX research of WebApp
* Streamline communication channels. Example: We platform is fine with help questions, but there are too many communication channels. Slack is not searchable and user friendly. 

SOP
* Transparent process for prioritizing bug/feature/UX requests
* Protocol for reporting bug/feature/UX 
* User manual or documentation on how to use webapp, particularly useful for on-boarding new AC
* Responsible data policy & security

August 
* Bring back the short proposal form for concept notes that are requesting less than 100k #717
* Create a new page template called "Results", that can be placed anywhere #1248
* Update the region scheme to the UN scheme and update all submissions accordingly #1173 
* Create a view of projects and fellows by geographic location (the map of where our support is going idea) #243 
* As a manager, the ability to customize available options from global fields when displayed on application #311
* Add a deadline field to determinations and include deadline in any notifications, if included #326
* Add a "Applications with deadlines" list to a users dashboard, listing submissions with deadlines for both applicants and the leads of those applications #306 
* As a manager, i need an easy way to track all set deadline dates given to an applicant or staff member #285
* As a reviewer, receive automated reminders for outstanding reviews assigned as deadlines approach #273

June-July
* Complete discovery and scoping for summer sprints
* Creation of [summer spring tickets](https://github.com/OpenTechFund/opentech.fund/issues?q=is%3Aopen+is%3Aissue+label%3Apost-approval) that focus on post approval workflows (project approval forms, contracting, payment requests, and regular project reporting) 
* Deploy API access for both users and projects
* Deploy ability for staff to apply labels to submissions (meta)
* Deploy first set of automation functions
* Performance and bug fixes always

From non-priority tickets in the current milestone ([2019-Q3 -priority](https://github.com/OpenTechFund/opentech.fund/issues?utf8=%E2%9C%93&q=is%3Aopen+is%3Aissue+-label%3Apriority+milestone%3A2019-Q3+))

* Harmonize the viability definitions and implement the same options for comments, reviews, and submissions
* Introduce an optional survey for applicants to complete post final-determination [#835](https://github.com/OpenTechFund/opentech.fund/issues/835)
* Allow users the ability to see and set their notification preferences in their profile
* Expose useful meta-data (avg amount approved, type of project, etc) from the API on internal and external pages (ie round and fund pages) 
* Improve the listing of projects, fellows, and other results on the public facing pages [#1248](https://github.com/OpenTechFund/opentech.fund/issues/1248)
* Begin offering the ability to associate a Signal number to receive and respond to notifications
* Ability for users to submit bug or feature requests from within the app or on error pages

### Discussions 
* What could the API/metadata inform us about current and future programming?
* What can we infer and what can we deduct from information we have at hand? Do we have complete picture and what are the gaps?

## Horizon 2
**_Approx. next 3 months_**

### Dev goals
Items from the current milestone ([2019-Q3](https://github.com/OpenTechFund/opentech.fund/milestone/2)) not included above or from the approaching milestone ([2019-Q4](https://github.com/OpenTechFund/opentech.fund/milestone/3)).

[todo, need to move items from above down here as is right and go through later milestone and creating high-level summaries]

* Introduce and test post approval features such as PAF, invoice, monthly report, creation/management
* Review and refine as needed the current responsible data policy
* Conduct a responsible data audit
* Change the repo name to an standalone project/app name and release a website highlighting the app itself
* Create a security information page outlining the security/privacy features of the app along with our ongoing guidelines for future features


### Discussions
* What are tangible outcomes from having better access to submission information? What materials do we need to meet objectives? Do we have sufficient capacity to implement activities?
* What further internal or external UX/UI exploratory sessions should we conduct and how best to share feedback with team, applicants, and the public?
* What additional information and communication do applicants need (ie guidance, messages/comms) and how do we improve our ongoing feedback loop with them?

## Horizon 3
**_Approx. next 6 months_**

### Dev goals
Items not above from the next two or three milestones.

[todo, still need to go through these milestones to create high-level summaries like above]

### Discussions

* Should we import all the manually created PAF's into the app for a PAF central database?
* What additional tools or resources do for applicants to navigate various funds, see #697?
  * Training and how-to materials for external stakeholders

## Horizon 4
**_Approx. next 12 months_**

### Dev goals
Items not above from the next three or four milestones.

[todo, still need to go through these milestones to create high-level summaries like above]

### Discussions
* What are our goals one year from now?

The [Following Progress page](https://github.com/OpenTechFund/opentech.fund/wiki/Following-progress) outlines how one can observe, watch, or follow the progress towards the above goals.

# Long-term goals by theme (epics)

In no particular order, we've listed long-term goals for the app below:

* Completely API-driven allowing multi-medium interface and easier 3rd party system integrations
* Managers ability to create and customize application workflows (this is currently a developer task)
* Applicants ability to submit end-to-end encrypted information via submission forms
* Federation between instances, ability for different entities to collectively engage on a shared fund
* Automated analysis on submissions for common things reviewers manually research/do (repo health, sentiment, community, etc)
* Support for collaborative / multi-user applications
* Proving options for peer review workflow (applicants reviewing other applications), other community-wide inputs, and collective decision making functions
* Automated reports on round, fund, and instance wide data (kpi's, application trends, etc)
* Integration of online contract/grant agreement signing, payment processing, and monitoring systems
* Managers ability to create, customize, and deploy a projects reporting format, workflow, and rhythm
* Bi-directional engagement via all notification mediums (ability to respond via email, slack, signal)
* Increase access control for most sensitive areas/functions (ie restrict based on device, security key, etc)
* Ability to deploy automated tests on 3rd party systems to ensure application functions and access permissions are working
* Interface that allows managers to set conditions for automatically progressing applications from one state to another
* Support for instance themes on the frontend
* Ability for creators of content (applicants and reviews) to control the visibility of their content
* Content wide support for saving drafts (even for anon applicants) and working offline
* Integration with discourse for community engagement (receiving answers from FAQ, asking questions, posting comments)
* Creation of a recommendation engine for assigning reviews to managers and reviewers
* Fully functional responsive Progressive Web App for mobile/tablets (think you can put on your home screen)
* Creation of a recommendation engine to provide initial suggestions if submissions are in/out of remit
* Creation of a prediction engine to indicate an submissions likelihood of progressing  
