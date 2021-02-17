# Purpose of this document
* Establish a shared sense of priority
* Clarify time-based expectations for next-steps and milestones
* Define terms reference for high-level structural elements
* Clarify bottom-liners for themes > goals (initiatives) > milestones
* Aid in the identification of resource needs and constraints

# Themes
**How they are organized:**

Theme (Vision / Very high level)

_{meta: priority [], label [], arch/owner [], devs: [], ui/ux: []; qa: []}_
* Initiatives (Goal)
  * Epics (Milestones / Objectives)
    * Stories (Issues / Tasks)

_**(not in order of priority, tbd)**_

## API 
_{meta: priority [], label [[api](https://github.com/OpenTechFund/hypha/labels/api)], arch/owner [], devs: [], ui/ux: []; qa: []}_
* Fully API-driven front-end
  * apply/ is completely replaced by the React app
  * Ability for others to create completely different apply/ alternatives
* Fully documented API
* R/W API access for 3rd party integrations
* API permissions interface in admin
* Begin exposing admin functions via API

## Portfolio management, post-approal, and project management
_{meta: priority [], label [[portfolio](https://github.com/OpenTechFund/hypha/labels/portfolio)], arch/owner [], devs: [], ui/ux: []; qa: []}_
* 

## 3rd party integrations 
_{meta: priority [], label [[integration](https://github.com/OpenTechFund/hypha/labels/integration)], arch/owner [], devs: [], ui/ux: []; qa: []}_
* Contract and payment management services (Salesforce, Sage, Netsuite, etc)
* Messaging and communication services
* 2-way engagement between channels
* Delivery confirmation w/in hypha
* Data portability, export/import
* Honorarium management services
* Help/Feedback services

## Security and privacy
_{meta: priority [], label [[privsec](https://github.com/OpenTechFund/hypha/labels/privsec)], arch/owner [], devs: [], ui/ux: []; qa: []}_
* Full db encryption
* PII handling
* Sensitive content handling
  * End-to-end encrypted field data
* Policy (GDPR/CCPA) management, compliance, consent
* Annual 3rd party security/privacy code audit
* Support for additional/multiple SSO providers with access rules
* Deploy a hypha.app wide (not just for OTF/Reset) bug bounty & disclosure service (ie bugcrowd, hackerone, etc)

## Metrics: Progress, performance, activity, and content
_{meta: priority [], label [[metrics](https://github.com/OpenTechFund/hypha/labels/metrics)], arch/owner [], devs: [], ui/ux: []; qa: []}_
* KPI’s for system, funds, rounds, managers, applicants
* KPI’s for system, portfolios, projects, contracts, managers, etc
  * Dashboard
  * Ability to make public/publish metrics publicly, to applicants, or all staff
* Application content trends
  * Improved content tagging/labeling/rating
  * Review and reviews labels/meta categories/ etc
* Improved search

## Participatory and collaborative processes
_{meta: priority [], label [[collab](https://github.com/OpenTechFund/hypha/labels/collab)], arch/owner [], devs: [], ui/ux: []; qa: []}_
* Peer review of applications (applicants reviewing applications)
* Community/network review of applications
* Collaborative applications
* Flash grants
* Ability to make an application publicly available
* Review and refine the “partners” role/functions

## Admin/management web interfaces
_{meta: priority [], label [[admin](https://github.com/OpenTechFund/hypha/labels/admin)], arch/owner [], devs: [], ui/ux: []; qa: []}_
* Full UI/UX audit and discovery for application management
* Full UI/UX audit and re-discovery for project management
* Put all user profile options/fields in one place or in both (admin/ or apply/)
* Create a built-in night-mode theme
* Support for “smart” application forms (ie available or required fields change based on what previous options were selected)

## Deployability of hypha
_{meta: priority [], label [[deploy](https://github.com/OpenTechFund/hypha/labels/deploy)], arch/owner [], devs: [], ui/ux: []; qa: []}_
* Build the hypha python/pip/django package
* Improve standalone docker install 
* Make it easy to theme/style/customize hypha public, admin, submission pages
* Support additional popular PaaS’s (ie Scalingo, etc)
* Begin development of  hypha SaaS (ie my.hypha.app)
* Increase the number of hypha deployments

## Developer onboarding process
_{meta: priority [], label [[devel](https://github.com/OpenTechFund/hypha/labels/devel)], arch/owner [], devs: [], ui/ux: []; qa: []}_
* Improve contributor guidelines, standards, practice docs
* Offer more reward/bounties

## Hypha org/community/brand
_{meta: priority [], label [[org](https://github.com/OpenTechFund/hypha/labels/org)], arch/owner [], devs: [], ui/ux: []; qa: []}_
* Have first annual hypha dev summit
* Fully migrate to standalone repository
* Refine hypha.app website
* Create standalone hypha community/support spaces

## Automation
_{meta: priority [], label [[auto](https://github.com/OpenTechFund/hypha/labels/auto)], arch/owner [], devs: [], ui/ux: []; qa: []}_
* Create a workflow/actions editor in the admin UI
* Create a message/notification editor in the admin UI for any missing ones
* Enable switches for all existing automations/actions
* Provide estimates to applicants on time to next stage
* Review recommendations (based on defined criteria)
* Suggested applications of interest (based on defined criteria)
* Auto screening > manual screening > auto determination > manual determination process

## Communication between managers and applicants
_{meta: priority [], label [[comms](https://github.com/OpenTechFund/hypha/labels/comms)], arch/owner [], devs: [], ui/ux: []; qa: []}_
* Create a notifications area in the web interface
* Create notification settings in account management
* Ability to comment on specific elements of the application workflow (application, reviews, submission responses)
* Ability to save and receive notification on new revisions without changing state
* A more structured/flexible back and forth alternative to submission responses
  * Ability for a team member (lead) to define submission-specific questions that reviewers are asked to respond to, in addition to the predefined review form.

## Not included but important
Things not to forget and/or bring up above
* Project reporting
* Encrypted field
* Localization/multilingual support
* Automated application insights
* Pagination of application forms
* Conditional logic forms (that bring you to previous defined pages/sections)

# Timeline
Goals, corresponding issues, and discussions are grouped into 3-month long milestones called horizons. Horizon 1 is the current milestone. Horizon 2 will be next, followed by horizon 3, then 4. This is all aspirational, hopefull, and approximate. 

## Horizon 1
[Issues](https://github.com/OpenTechFund/hypha/milestone/24) currently being worked on.
### Goals
### Discussions

## Horizon 2
[Issues](https://github.com/OpenTechFund/hypha/milestone/25) to be addressed in the next 3-6 months
### Goals
### Discussions

## Horizon 3
[Issues](https://github.com/OpenTechFund/hypha/milestone/26) to be addressed in the next 6-9 months
### Goals
### Discussions

## Horizon 4
[Issues](https://github.com/OpenTechFund/hypha/milestone/27) to be addressed in the next 9-12 months
### Goals
### Discussions
