
## Technical work updates
From @frjo

### New implementations
- changes applied specifically for OTF IFF fund
- If a user wants to change the thumbs up/down decision they now can.  
- Day option has been added to duration field
- Add number of filter results to the react app (I think this is right description)

## Others?
- Hypha Dev Summit - March 31 - April 1. Sign-up!

## Design and research work to discuss

### [2278](https://github.com/HyphaApp/hypha/discussions/2278)
Creating specific views for screening, reviewing for each separate funder may be a lot of work, that will not meet people's needs.
Instead, try a unified design so users can tailor the all applications view to meet their needs. This work is being tracked in [in this discussion thread](https://github.com/HyphaApp/hypha/discussions/2278).

The purpose of this view is to allow users to see the same list of applications, and to save unnecessary implementation.

**Next steps**
- we also want to have analytics on this section.
  - Action: Bernard to open a metrics ticket to measure usage of UI sections, what filters are used most in the design. It needs to have a track on each filter drop-down
- Action: Everyone to give feedback on the designs here: https://github.com/HyphaApp/hypha/discussions/2278
- Terminology for these different views/lists/displays

### [2262](https://github.com/HyphaApp/hypha/issues/2262)
Remove, or not, the item pagination on the submissions page?

**Decisions**
Remove! 

**Next steps**
- Nothing needed.

### [2263](https://github.com/HyphaApp/hypha/issues/2263)
Remove or not?

**Decisions**
remove! 

**Next steps**
- Nothing needed

### [2275](https://github.com/HyphaApp/hypha/issues/2275)
Automtically add wagtail systematic required questions to forms by default 

**Next steps**

### [2214](https://github.com/HyphaApp/hypha/issues/2214) 
Discuss. Is this part of Hypha WL? Do OTF need to use this?

**Next steps**
This is not needed by OTF right now. It would be nice to have at a later date.
Action: Bernard review the design implemented here: https://github.com/HyphaApp/hypha/issues/2214

### [2276](https://github.com/HyphaApp/hypha/issues/2276)[which was moved to a discussion](https://github.com/HyphaApp/hypha/discussions/2277)
Create a "concept note" feature that goes before the funds.
Discuss. This fund/category organisation would be purely internal. Discussed suggestions of how to do it.

Easiest to implement is to have 

The sticking point is 1) each fund can have only 1 review form, 2) if you want to segment single fund into different review form that needs to be implemented, 3)

Short term solution:
Have a single review form with distinct sections for each type of application category. Evaluate this in a few months.

Long term solution:
Based on how the short term solution goes, make 

Most important is: Single apply button and then splitting into categories.


### [2273](https://github.com/HyphaApp/hypha/issues/2273)
Single Button Apply Review Forms
The suggestion is to 
Discuss this at next weeks meeting.

### Adding multiple leads or better "easily see and get notifications about all applications that come in under category X"
Notifications needed for 