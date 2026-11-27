# Voting

The organization handles its votes via a Square-Root Proportional Weighting and Dual-Gate Quorum Instant Runoff Model.

## Voting Entities

The OGC has 2 types of voting entities:

- Member Organizations: Each recognized member organization size is calculated using a member roster.
- Unaffiliated Block: All unaffiliated members are collectively grouped into a single "Unaffiliated" voting block.

### Member Voting Eligibility

Only members with an email address on the roster can vote, and only they count towards the size of their entity.
<!--This rule exists thanks to Nero btw-->
A member listed in more than one organization counts for the first of those organizations in alphabetical order.

### Active Voting Entities

A voting entity is active if at least one of its members is eligible to vote under [Member Voting Eligibility](#member-voting-eligibility). Only active voting entities take part in a vote.

## Proportional Weighting

Each voting entity's voting power is calculated as follows:

```
voting power = √(size of the entity) ÷ sum of √(size) of every entity
```

The sum only includes entities that reached [Internal Quorum](#internal-quorum). An entity that did not reach internal quorum has no voting power.

For the unaffiliated block, the number of individuals who cast a vote, abstentions included, is considered the size of the block. This allows the unaffiliated block to always meet [Internal Quorum](#internal-quorum) as long as at least one unaffiliated member votes.

### Internal Voting Power Distribution

In the case that the internal votes within a [Voting Entity](#voting-entities) disagree with themselves, the voting power of the entity is distributed evenly amongst the members who voted and the stance of the entity is formulated according to the proportion of options its members voted for.

## Dual-Gate Quorum

### Internal Quorum

A member organization's vote is only counted if at least **50%** of its internal roster participated in formulating its stance. [Abstentions](#abstentions) count as participating.

### Coalition Quorum

At least **50%** of all [Active Voting Entities](#active-voting-entities), rounded up, must reach internal quorum during the [Voting Window](#voting-window). If the coalition quorum is not met, the vote is [Void](#void) and rescheduled to a later date.

## Instant Runoff

For decisions where there are more than 2 options, members will rank each option and the final vote will be calculated using an instant runoff model. An option wins once it holds more than half of the total voting power of the ranked votes. The lowest ranking option(s) are discarded and the next choice of the discarded votes is added to the tally of the remaining options. This repeats until a majority consensus is reached OR two or fewer options remain without a majority consensus, in which case the vote has [No Majority](#no-majority).

### Tying for last

In the event more than 1 option ties for last place, all of them will be discarded in one round. If every remaining option is tied, they are not discarded and the vote ends as a [Tie](#tied).

### Ranking

Members will rank the options as they see fit. A member may choose to exclude an option they don't want from their rankings. In the event all of the member's ranked choices are exhausted, the member's vote no longer backs any option, but its voting power still counts towards the total that an option needs more than half of. Unlike an [Abstention](#abstentions), an exhausted vote can therefore stop any option from reaching a majority.

## Abstentions

A member may choose to abstain from a vote. Such an abstention will count as having shown up and will assist the [Voting Entity](#voting-entities) the member is part of to reach its internal quorum and have the vote of the rest of the members counted. The abstaining member receives their share of the entity's voting power like any other voter, and that share is then left out of the total. The remaining votes of every entity therefore make up the whole of the result.

## Voting Window

The motion is expected to include a voting window in the [Motion Format](#motion-format). In the event a voting window is not mentioned, a default of 24 hours will be used as the voting window. The window starts when the motion is sent, and a vote sent at the moment the window closes still counts.

## Outcomes

### Passed

An option holds more than half of the total voting power of the ranked votes.

### No Majority

No option reached a majority before two or fewer options remained, and the remaining options are not [Tied](#tied). The vote will be rescheduled.

### Tied

Every remaining option is tied. The vote has to be held again.

### Void

The [Coalition Quorum](#coalition-quorum) was not met. The vote will be rescheduled.

## Automation

The counting of votes will be done by an automated system. The system will follow all voting rules mentioned in this document and must be available for all members of the org to view and audit and request changes on if the system does not adhere to the specification described here.

## Voting Medium

Voting will be carried out over mail on the `governance` mailing list. The motion and the votes must adhere to certain rules:

### Motion Format

- The motion must end with a "Vote Below This Line" statement followed with a line consisting of dashes (-). Members are expected to vote below this line.
- The motion is expected to include the voting window in the format "Open for X `period`" where period may be any of `hours`, `days` or `weeks`. This is optional and a default of 24 hours will be used if this is missing.
- The motion must clearly label every option voted on in the format "Option X: `title`". A motion needs at least 2 options.

### Voting Format

- Members must vote from the email address listed for them on the roster.
- Members must quote the body of the motion and reply directly to the motion instead of replying to the next person after.
- Members must cast their vote on the first line below the line specified in the [Motion Format](#motion-format).
- Members must cast their vote in the format of "Option X" or simply "X". For ranking options, the format may be used as "Option X > Option Y" or simply "X > Y". To abstain, members write "Abstain" instead.
- Any other words, an option that is not in the motion, or an option ranked twice will mark the vote rejected and the member may try again to cast a valid vote.
- A member's last valid vote within the [Voting Window](#voting-window) is the one that counts. A rejected vote does not replace an earlier valid one.
