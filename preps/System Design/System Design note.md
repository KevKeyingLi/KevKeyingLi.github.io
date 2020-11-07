# 
This is the first note for system design. I will start using it as a initial draft, and when more structured notes come in, this should be updated and moved to other notes.

## steps of an intervew
### Problem description: interviewer state the problem
* interviewer state the problem
* ask clarifications
    - all kinds of sizes
        + user number simultaneously
        + data size
    - operation distribution
        + how much are each type of operation
        + read/write distribution
    - login & session
    - details
        + type of content. text, image, video
* restate the problem, and get confirmation of assumptions

Example
> • Will users of our service be able to post tweets and follow other people?
> • Should we also design to create and display the user’s timeline?
> • Will tweets contain photos and videos?
> • Are we focusing on the backend only or are we developing the front-end too?
> • Will users be able to search tweets?
> • Do we need to display hot trending topics?
> • Will there be any push notification for new (or important) tweets?
### Tackle the problem
#### start with a initial design with basic structure

####
