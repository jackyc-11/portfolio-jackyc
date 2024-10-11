---
title: Assignment 4 (Alpha)
layout: doc
---

# Backend Design & Implementation

[Backend Code Repository (GitHub)](https://github.com/jackyc-11/6.1040-fa24-backend)

[Deployed Service (Vercel)](https://tether1040.vercel.app/)

## Concepts
1) **Authenticating**

*Purpose:* <br>
Authenticate users so that app users correspond to people.

*Operational Principle:* <br>
After a user registers with a username and password pair, they can authenticate as that user by providing the same pair of username and password.

*State:*
```
registered: set User
username, password: registered -> one String
```

*Actions:*
```
register(name, pass: String, out user: User):
    if (name, pass) not in registered:
        registered += new User(name, pass)
authenticate(name, pass: String, out user: User):
    user = {u ∈ registered | u.username = name ∧ u.password = pass}
```

2) **Sessioning**

*Purpose:* <br>
Enable authenticated actions for an extended period of time.

*Operational Principle:* <br>
After a session starts and before it ends (manually ended or automatically timed out), the getUser action returns the user identified at the start.

*State:*
```
active: set Session
user: active -> one User
```

*Actions:*
```
start(user: User, out sess: Session):
    active += new Session(user)
getuser(sess: Session, out user: User):
    user = user(sess)
end(sess: Session):
    active = active \ {sess}
```

3) **Texting**

*Purpose:* <br>
Enable users to send and receive textual messages.

*Operational Principle:* <br>
After a user sends a message to another user, the recipient can read the message.

*State:*
```
messages: set Message
sender, recipient: messages -> one User
content: messages -> one String
timestamp: messages -> one Time
```

*Actions:*
```
send(sender: User, recipient: User, content: String, out message: Message):
    messages += new Message(sender, recipient, content, currentTime())
receive(recipient: User, sender: User, out message: Message):
    message = {m ∈ messages | m.recipient = recipient ∧ m.sender = sender}
```

4) **Video Calling**

*Purpose:* <br>
Allow users to engage in real-time video communication.

*Operational Principle:* <br>
When a user initiates a video call and the recipient accepts, both users (caller and recipient) can see and hear each other until one of them ends the call.

*State:*
```
activeCalls: set Call
caller, recipient: activeCalls -> one User
startTime, endTime: activeCalls -> one Time
```

*Actions:*
```
startCall(caller: User, recipient: User, out call: Call):
    activeCalls += new Call(caller, recipient, currentTime())
endCall(call: Call):
    call.endTime := currentTime()
```

5) **Mood Mapping**

*Purpose:* <br>
Allow users to set and display a status or emotional state.

*Operational Principle:* <br>
Users can select an emoji to represent their mood or status, which will be displayed to the chat until updated or removed.

*State:*
```
moods: set Mood
user: moods -> one User
```

*Actions:*
```
setMood(user: User, out mood: Mood):
    if user ∈ moods:
        moods(user).mood := mood
    else:
        moods += new Mood(user, mood)
removeMood(user: User):
    moods = moods \ {mood | mood.user = user}
```

6) **Post-It Walling**

*Purpose:* <br>
Allow users to create and display short posts on a virtual wall.

*Operational Principle:* <br>
Users can post notes or messages on their wall, and these posts remain visible until they are removed by the user.

*State:*
```
posts: set Post
author: posts -> one User
content: posts -> one String
```

*Actions:*
```
createPost(author: User, content: String, out post: Post):
    posts += new Post(author, content)
deletePost(post: Post):
    posts = posts \ {post}
viewWall(user: User, out posts: set Post):
    posts = {p ∈ posts | p.author = user}
```

7) **Friending**

*Purpose:* <br>
Allow users to establish connections with other users, forming a mutual friendship.

*Operational Principle:* <br>
A user can send a friend request to another user. If accepted, the two users become friends, allowing them to interact with different features in the app.

*State:*
```
friends: set Friendship
user1, user2: friends -> one User
pendingRequests: set Request
sender, recipient: pendingRequests -> one User
```

*Actions:*
```
sendFriendRequest(sender: User, recipient: User, out request: Request):
    pendingRequests += new Request(sender, recipient)
acceptFriendRequest(request: Request, out friendship: Friendship):
    pendingRequests = pendingRequests \ {request}
    friends += new Friendship(request.sender, request.recipient)
rejectFriendRequest(request: Request):
    pendingRequests = pendingRequests \ {request}
removeFriend(friendship: Friendship):
    friends = friends \ {friendship}
```

**Other Potential Concepts:** What's Cooking, Counting Down, Weather Tracking

## Global Data Model
```
app Tether

include Authenticating as Auth
let User = Auth.User
include Sessioning[User]
include Texting [User, Message]
include MoodMapping[User]
include Friending[User]
inclue VideoCalling[User, Call]
```

## Data Diagram
![](a4_media_files\data_diagram.jpg)