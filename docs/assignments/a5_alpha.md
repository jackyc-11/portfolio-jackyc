---
title: Assignment 5 (Alpha)
layout: doc
---

# Frontend Design & Implementation

[Frontend Code Repository (GitHub)](https://github.com/jackyc-11/61040-fa24-frontend)

[Deployed Frontend (Vercel)](https://tetherfrontend.vercel.app/)

## Heuristic Evaluation

**Usability Criteria**

*Discoverability:* how rapidly and easily can users understand how to operate the interface?

- Support: The chat bubble and person icon are visually distinct and intuitive, so their purpose should be easy for users to understand.
- Support: Elements (both nouns and verbs) are well labeled to clarify their functions.
- Violation: For mood mapping, users may be confused because they are expected to type in a mood, but for features like this, they are typically shown a dropdown to select from.
- Violation: The person icon for friends and the person icon for profile are similar, although they're placed in different parts of the left navigation bar. I could potentially choose a more fitting icon for friends, such as an icon with two or more people.
- Violation: Important concepts/actions are hidden by an ellipsis icon. A potential solution is to get rid of the ellipsis and represent each concept/action on the same bar with an icon (e.g. mood mapping with a smiley face). 
- Tradeoff (for violation directly above): There will no longer be text that specifically says "Mood Mapping", so users may be confused about the purpose of the icons. In that case, does the potential solution really benefit discoverability?
- Tradeoff: Adding tooltips or onboarding tours may improve learnability but may be extraneous for users who have a more intuitive sense of using the product, as most of us may know from clicking "Next" on the Figma basics tour 😂.

*Error Tolerance:* how easily can a user recover from making mistakes?

- Support: Users are able to unsend a message if they accidentally sent it to the wrong person.
- Support: Users can edit a message if the content is incorrect.
- Support: Posts and moods can be edited or removed, similar to messages.
- Support: Users can cancel a friend request if they accidentally sent it to the wrong person.
- Support: Users who accidentally start a video call can easily end the call.
- Violation: There is currently no confirmation dialog or undo feature when deleting a post or removing a friend.
- Tradeoff: While adding confirmation dialogs or undo features increases error tolerance, it also introduces extra friction for users who are sure of their actions, reducing efficiency to an extent.

**Physical Heuristics**

*Fitt's Law:* how quickly and easily can users reach for (or point to with their cursor) interface elements?

- Support: The short drop-down menu from selecting a concept/action (ellipsis icon to access Mood Mapping, Post-It Wall, Weathering With You) minimizes the user's travel distance in selecting an option.
- Support: Although the profile button may be somewhat small, it is almost all the way on the bottom left, so users can swing their cursor there to get quick access.
- Support: The size of each chat and the buttons are relatively large for users to easily move their cursor to and click on.
- Support: Items are placed in areas where users would generally expect them. For example, the textbox and send message are placed at the bottom. The button to end call is placed on the rightmost of the other call-related buttons.
- Violation: The ellipsis and video call icon are next to each other, so users may fat finger and accidentally call another user when they were actually trying to access another concept/action.
- Tradeoff: While increasing size of icons and elements may make them easier to click on, it may also make it more difficult to keep the interface visually clean.


*Gestalt principles:* does the layout of the interface elements convey conceptual structure?

- Support: Conceptual structure is established through common regions and proximity. For instance, the list of chats and the texting area are in their own rectangular bubbles. Grouping related objects together in a closed area helps separate them from other groups.
- Support: The background of the page contrasts with the rectangular bubbles, making the content in the rectangular bubbles the foreground while the background fades away.
- Support: Our brains tend to favor symmetrical forms. The spacing between each tab, chat, friend, request, etc. is evenly spaced.
- Violation: The scattered nature of the Post-It Wall, with no clear alignment of the notes, may violate symmetry and common fate, potentially confusing users about where to find specific posts or whether certain notes are related to one another.
- Tradeoff (for violation directly above): I think the freeform layout gives users a more realistic experience as if they were realistically placing a post-it note. Grouping can also be done using the colors of the post-it notes.

**Linguistic Level**

*Speak a user's language:* does the interface use simple, helpful informative messages? are there instances where messages might only be understandable by developers?

- Support: Buttons are consistently labeled with action verbs, such as "Add friend", "Cancel Request", "Remove", etc., to clarify their functions.
- Support: Tabs and concepts/actions are clearly labeled, so users know where they are navigating to.
- Tradeoff: Adding instructional text could clutter the interface and detract from the minimalist design. A good compromise might be have a help page that offers a brief tutorial.

*Consistency:* does the interface reuse the same names, symbols, and icons for the same concepts or actions? how consistent is the interface with others across the same application domain or platform?

- Support: Icons are well associated with its respective action. For example, add friends has an icon with a person and a search magnifying glass. Messages has a chat bubble icon.
- Support: The interface shouldn't be difficult to navigate for users who have used social media apps before since it is similar with the interface of others across the same application domain.

## Visual Design Study