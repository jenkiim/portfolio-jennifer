---
title: "Assignment 4: Backend Design"
layout: doc
---

# Assignment 4: Backend Design
#### Collaboration Partners: Tiana Jiang
## Abstract Data Models
**concept:** Responding [Author, Item]

<!-- **purpose:** share opinions on text, which allows for discussions and learning of different perspectives

**principle:** after a piece of text is posted, an opinion on the piece of text can be written and shared -->

**state:**

responses: set Response

title: responses -> one String

content: responses -> one String

author: responses -> one Author

target: responses -> one Item
<!-- 
**actions:**

```
createResponse(content: String, user: User, target: Target, out response: Response)
    make a new Response that corresponds to the title, text, the user who wrote the Response,
    the issue the response is for, and the side of the issue the response is arguing for.
    The default vote amount is 0.

deleteResponse(user: User, response: Resonse)
    delete the specified response made by the User. The user must have been the author of response before this.
``` -->

---

**concept:** Topicing [Author]

**state:**

topics: set Topic

author: topics -> one Author

title, description: topics -> one String

---

**concept:** Authenticating

**state:**

registered: set User

username, password: registered -> one String

---

**concept:** Sessioning-[User]

**state:**

active: set Session

user: active -> one User

---

**concept:** Sideing [Issue, User]

**state:**

sides: set Side

degree: sides -> one OpinionDegree //*8 possible opinion degrees (strongly disagree, disagree, slightly disagree, neutral, slightly agree, agree, strongly agree, undecided) for every issue*

issue: sides -> one Issue

users: sides -> set User

---

**concept:** Labeling [Item]

**state:**

labels: set Label

title: labels -> one String

items: labels -> set Item

---

**concept:** Upvoting [Item, User]

**state:**

upvotes, downvotes: Item -> set User

count: Item -> one Integer //*number of upvotes - downvotes*

### Data Model

![Data Model](./datamodel.png){:width="600"}

#### App Definition
app  **POV**
- include Responding [Authenticating.User, Topicing.Topic] as RespondingToTopic
- include Responding [Authenticating.User, RespondingToTopic.Response + RespondingToResponse.Response] as RespondingToResponse
- include Topicing [Authenticating.User]
- include Authenticating
- include Sessioning-[Authenticating.User]
- include Sideing [Topicing.Topic, Authenticating.User]
- include Labeling [RespondingToTopic.Response] as ResponseLabeling
- include Labeling [Topicing.Topic] as TopicLabeling
- include Upvoting [RespondingToTopic.Response + RespondingToResponse.Response, Authenticating.User]
<!-- - include Upvoting [Topicing.Topic, Authenticating.User] as TopicUpvoting -->

## Backend Code

[Link to github repo](https://github.com/jenkiim/6104-backend)

## Deployed Backend

[Link to deployed site](https://6104-backend.vercel.app)


- whether to have undecided separately on sideing concept
- sideing concept -> 8 sides for each topic -> strongly disagree, disagree, slightly disagree, neutral, slightly agree, agree, strongly agree, undecided
    - including undecided


- response to topic
- response to response (two separate instances?)
- upvoting topics?
- responses have targets, not responsesToResponses
- description for topics? editing for topics? deleting for topics?
- nvmmmmm: need a get method for responses to responses for users? 

- can only create tag when adding it to post? or just create tag?

- data model diagram
    - can i reuse item for the target in responding concept and in upvotiing concept![alt text](<Note Oct 2, 2024.png>)