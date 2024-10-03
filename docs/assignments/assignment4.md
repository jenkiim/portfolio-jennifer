---
title: "Assignment 4: Backend Design"
layout: doc
---

# Assignment 4: Backend Design
#### Collaboration Partners: Tiana Jiang, ChatGPT
## Abstract Data Models
**concept:** Responding [Author, Target]

<!-- **purpose:** share opinions on text, which allows for discussions and learning of different perspectives

**principle:** after a piece of text is posted, an opinion on the piece of text can be written and shared -->

**state:**

responses: set Response

content: responses -> one String

author: responses -> one Author

target: responses -> one Target
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

degreeOfSide: sides -> one OpinionDegree //*8 possible opinion degrees (strongly disagree, disagree, slightly disagree, neutral, slightly agree, agree, strongly agree, undecided) for every issue*

issue: sides -> one Issue

usersOfSide: sides -> set User

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

![Data Model](){:width="600"}

#### App Definition
app  **POV**
- include Responding [Authenticating.User, Topicing.Topic] as RespondingToTopic
- include Responding [Authenticating.User, Responding.Response] as RespondingToResponse
- include Topicing [Authenticating.User]
- include Authenticating
- include Sessioning-[Authenticating.User]
- include Sideing [Topicing.Topic, Authenticating.User]
- include Labeling [Responding.Response] as ResponseLabeling
- include Labeling [Topicing.Topic] as TopicLabeling
- include Upvoting [Responding.Response, Authenticating.User] as ResponseUpvoting
<!-- - include Upvoting [Topicing.Topic, Authenticating.User] as TopicUpvoting -->

## Backend Code

[Link to github repo](https://github.com/jenkiim/6104-backend)

## Deployed Backend

[Link to deployed site](https://pov-mmo9bd0r3-jenkiims-projects.vercel.app)


- whether to have undecided separately on sideing concept
- sideing concept -> 8 sides for each topic -> strongly disagree, disagree, slightly disagree, neutral, slightly agree, agree, strongly agree, undecided



- response to topic
- response to response (two separate instances?)
- upvoting topics?
- responses have targets, not responsesToResponses
- description for topics? editing for topics? deleting for topics?

- can only create tag when adding it to post? or just create tag?