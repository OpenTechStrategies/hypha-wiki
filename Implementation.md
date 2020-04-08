# Implementation of the principles

## Media

Media is encouraged to be split into two distinct storage locations. A Public and a Private location, applicant media should exist only in the Private location. This is for two reasons:

1. This separates the site media, which is served publicly with no authentication, from the Applicant media, which has permissions checks, it reduces the risk of a miss-configured storage exposing the Applicant data.

2. Maintains separation between the two halves of the platform, Apply and Public.

Media should also be served from a view that inherits from the [PrivateMediaView](https://github.com/OpenTechFund/hypha/blob/master/hypha/apply/utils/storage.py) which will confirm that the file isn't made public and can be configured to return the file object from an authenticated view.
