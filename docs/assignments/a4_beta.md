---
title: Assignment 4 (Beta)
layout: doc
---

# Backend Design & Implementation

[Backend Code Repository (GitHub)](https://github.com/jackyc-11/6.1040-fa24-backend)

[Deployed Service (Vercel)](https://tether1040.vercel.app/)

## Concepts
**Authenticating**

*State:*
```
registered: set User
username, password: registered -> one String
```

**Sessioning [User]**

*State:*
```
active: set Session
user: active -> one User
```

**Texting [User, Message]**

*State:*
```
messages: set Message
sender, recipient: messages -> one User
content: messages -> one String
```

**Video Calling [User, Call]**

*State:*
```
activeCalls: set Call
caller, recipient: activeCalls -> one User
status: activeCalls -> one String
```

**Mood Mapping [User, Mood]**

*State:*
```
moods: set Mood
mood: moods -> one String
user, recipient: moods -> one User
```

**Posting [User]**

*State:*
```
posts: set Post
author, recipient: posts -> one User
content: posts -> one String
```

**Friending [User]**

*State:*
```
friends: set Friendship
requests: set Request
user1, user2: friends -> one User
from, to: requests -> one User
status: requests -> one String
```

**Weathering [User, Weather]**

*State:*
```
shares: set WeatherShare
user: shares -> one User
agreed: shares -> one Boolean
city: shares -> optional String
state: shares -> optional String
```

## Global Data Model
```
app Tether

include Authenticating as Auth
let User = Auth.User
include Sessioning[User]
include Friending[User]
include Posting[User]
include Texting [User, Message]
include MoodMapping[User, Mood]
include VideoCalling[User, Call]
include Weathering[User, Weather]
```

## Data Diagram
![](a4_media_files\data_diagram2.jpg)

## Design Reflection
For the Mood Mapping concept, I was initially planning to explore an emoji API that would display a dropdown or picker from which users could select their moods. However, I ultimately chose to simplify the implementation by allowing the mood to be a string restricted by a regex to only allow emoji inputs. The motivation behind this decision is that modern smartphone and desktop keyboards already have built-in emoji functionality, making it easy for users to input emojis directly. A simple alternative I considered was using a predefined set of emojis but rejected this option as it limited the expressiveness of users. Additionally, mood doesn't just mean facial emojis; I wanted to allow users to express more than just their feelings, from activity to food to anything that can be expressed by an emoji.

For the Video Calling concept, I initially had a reject call and end call action. The reject call action is to deny an incoming call, and the end call action is to terminate an ongoing call. I was thinking if there's really a difference between the two since if a user sends someone a call, the recipient can "reject" or "end" the call, both of which terminates the call. I decided to just omit the reject call action since I felt it was redundant.

For the Weathering concept, the idea was to use APIs to get user location, which would then be used to get the weather. The hope was to use the API to access the client IP for location access, but Vercel intentionally blocks the client IP to prevent spoofing, so the location API always returns Virginia where the Vercel servers are hosted. I chose to go with a less convenient way to get the location (city and state) via manual input. The location is then fed to the weather API. Furthermore, there were privacy concerns over users using other users' locations nefariously. As a result, I integrated a Turn on Share action as a no-use option for users who feel uncomfortable sharing their location.