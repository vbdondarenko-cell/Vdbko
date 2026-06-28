# LINKUP
## Complete Information Architecture Document
### Version 1.0 | Professional UX Architecture

---

# DOCUMENT OVERVIEW

This document defines the complete Information Architecture for LinkUp, documenting every screen, component, action, and navigation flow across all 20 ecosystems.

**Scope:** 180 unique screens across 20 ecosystems
**Target Users:** Design team, Product team, Engineering team, QA team
**Last Updated:** June 2026

---

# NAVIGATION STRUCTURE

## Global Navigation

```
┌─────────────────────────────────────────────────────────────────┐
│                    BOTTOM TAB BAR                                │
├──────────┬──────────┬──────────┬──────────┬──────────┬────────┤
│   Home   │  Explore  │   (+)    │  Inbox   │  Profile │  Menu  │
│   (Feed) │          │  (Create)│  (Chat)  │          │        │
└──────────┴──────────┴──────────┴──────────┴──────────┴────────┘
```

## Secondary Navigation

```
├── Profile Header (Swipe down from top)
├── Story Ring (Horizontal scroll above feed)
├── Activity (Swipe up/notification badge)
├── Map (Location icon in header)
├── Settings (Profile menu → Gear icon)
└── Search (Search icon in header)
```

---

# ECOSYSTEM 1: AUTHENTICATION (15 Screens)

## 1.1 Splash Screen
**Purpose:** Brand introduction and session check
- **Entry Points:** App launch
- **Exit Points:** 
  - → Welcome Screen (new users)
  - → Home Feed (returning users with valid session)
  - → Biometric Screen (returning users with biometric enabled)
- **Components:** App logo, Loading indicator, Background gradient
- **Actions:** Auto-redirect based on session state
- **Navigation:** Automatic transition (no user interaction)

## 1.2 Welcome Screen
**Purpose:** Marketing introduction and login/signup prompts
- **Entry Points:** Splash (new user), Onboarding completion
- **Exit Points:**
  - → Login Screen (tap Login)
  - → Signup Screen (tap Sign Up)
  - → Privacy Policy (tap link)
  - → Terms of Service (tap link)
- **Components:** Hero carousel, Feature highlights, Login button, Signup button, Language selector, Skip link
- **Actions:** Swipe carousel, Tap buttons, Select language
- **Navigation:** Modal push for auth screens

## 1.3 Login Screen
**Purpose:** Existing user authentication
- **Entry Points:** Welcome (tap Login), Forgot Password link
- **Exit Points:**
  - → Home Feed (successful login)
  - → MFA Challenge (if enabled)
  - → Forgot Password (tap link)
  - → Signup Screen (tap Sign Up link)
- **Components:** Email/phone input, Password input, Show/hide password toggle, Login button, Forgot password link, Social login buttons, Back arrow
- **Actions:** Type credentials, Toggle password visibility, Submit login, Navigate to signup
- **Navigation:** Push to MFA or Home, Modal for signup

## 1.4 Signup Screen
**Purpose:** New user registration
- **Entry Points:** Welcome (tap Sign Up), Login (tap link)
- **Exit Points:**
  - → Phone Verification (enter phone)
  - → Email Verification (enter email)
  - → Login Screen (tap Login link)
- **Components:** Name input, Username input, Email/phone input, Password input, Date of birth picker, Terms checkbox, Signup button, Social login buttons
- **Actions:** Fill form, Validate username availability, Submit signup, Navigate to login
- **Navigation:** Push to verification

## 1.5 Phone Verification Screen
**Purpose:** Verify phone number via OTP
- **Entry Points:** Signup (phone selected), Settings (phone change)
- **Exit Points:**
  - → Onboarding (success)
  - → Resend OTP (tap link)
  - → Change Number (tap link)
  - → Login Screen (cancel)
- **Components:** Phone number display, OTP input (6 digits), Timer countdown, Resend button, Change number link, Support link, Back arrow
- **Actions:** Enter OTP, Auto-submit on complete, Resend code, Change number
- **Navigation:** Push to Onboarding, Modal for change number

## 1.6 Email Verification Screen
**Purpose:** Verify email via link click
- **Entry Points:** Signup (email selected), Settings (email change)
- **Exit Points:**
  - → Onboarding (click verification link)
  - → Resend Email (tap link)
  - → Change Email (tap link)
  - → Login Screen (cancel)
- **Components:** Email address display, Instruction text, Open email button, Resend button, Change email link, Timer countdown, Back arrow
- **Actions:** Open email app, Resend verification, Change email
- **Navigation:** Deep link to email, Push to Onboarding

## 1.7 MFA Challenge Screen
**Purpose:** Two-factor authentication verification
- **Entry Points:** Login (MFA enabled), Critical action
- **Exit Points:**
  - → Home Feed (success)
  - → Backup Code Entry (tap link)
  - → Login Screen (cancel)
- **Components:** Method indicator (SMS/Authenticator), Code input, Timer, Remember device checkbox, Backup code link, Back arrow
- **Actions:** Enter code, Auto-submit, Use backup code
- **Navigation:** Push to Home, Modal for backup code

## 1.8 Backup Code Entry Screen
**Purpose:** Alternative authentication via backup codes
- **Entry Points:** MFA Challenge (tap link)
- **Exit Points:**
  - → Home Feed (valid code)
  - → MFA Challenge (invalid code)
- **Components:** Backup code input, Submit button, Code list display, Warning text
- **Actions:** Enter backup code, Submit, View remaining codes
- **Navigation:** Push to Home, Pop to MFA Challenge

## 1.9 Forgot Password Screen
**Purpose:** Password recovery initiation
- **Entry Points:** Login (tap link)
- **Exit Points:**
  - → Phone/Email (enter identifier)
  - → Login Screen (cancel)
- **Components:** Email/phone input, Submit button, Remember password link, Back arrow
- **Actions:** Enter identifier, Submit recovery request
- **Navigation:** Push to Reset Password

## 1.10 Password Reset Screen
**Purpose:** Set new password after verification
- **Entry Points:** Forgot Password (link in email/SMS)
- **Exit Points:**
  - → Login Screen (success)
  - → Session Expired (link expired)
- **Components:** New password input, Confirm password input, Show/hide toggles, Password strength indicator, Reset button, Back arrow
- **Actions:** Enter new password, Confirm, Validate strength, Submit reset
- **Navigation:** Push to Login

## 1.11 Biometric Setup Screen
**Purpose:** Enable FaceID/TouchID/Fingerprint
- **Entry Points:** Onboarding (step), Settings → Security
- **Exit Points:**
  - → Onboarding (enable)
  - → Skip → Onboarding/Settings
- **Components:** Biometric icon, Explanation text, Enable button, Skip button, Back arrow
- **Actions:** Enable biometric, Skip for now
- **Navigation:** Push forward, Pop back

## 1.12 Biometric Prompt Screen
**Purpose:** Authenticate via biometrics
- **Entry Points:** App launch, Critical action
- **Exit Points:**
  - → Home Feed (success)
  - → Login Screen (failure/cancel)
  - → Fallback → PIN entry
- **Components:** Biometric icon, Prompt text, Cancel button, Use password link
- **Actions:** Scan face/fingerprint, Cancel, Use password
- **Navigation:** Push to Home, Modal to password

## 1.13 Session Management Screen
**Purpose:** View and manage active sessions
- **Entry Points:** Settings → Security → Active Sessions
- **Exit Points:**
  - → Session Detail (tap session)
  - → Settings (back)
- **Components:** Session list, Current device indicator, IP address, Last active, Location, Logout all button, Back arrow
- **Actions:** View sessions, Tap for details, Logout individual, Logout all
- **Navigation:** Push to detail, Pop to settings

## 1.14 Session Detail Screen
**Purpose:** View specific session information
- **Entry Points:** Session Management (tap session)
- **Exit Points:**
  - → Report Issue (tap link)
  - → Session Management (back)
- **Components:** Device name, Device type icon, IP address, Location, Browser/app, Last active timestamp, Login time, Logout button, Report button
- **Actions:** View details, Logout this session, Report suspicious activity
- **Navigation:** Pop to list

## 1.15 Onboarding Screen (Multi-step)
**Purpose:** Initial user setup and preferences
- **Entry Points:** Verification complete, First app launch
- **Exit Points:**
  - → Profile Setup (step 1)
  - → Interest Selection (step 2)
  - → Notification Setup (step 3)
  - → Privacy Setup (step 4)
  - → Home Feed (complete)
- **Components:** Progress indicator, Step content, Next button, Skip button, Back button
- **Actions:** Complete steps, Skip optional steps, Navigate between steps
- **Navigation:** Horizontal page swipe, Linear progression

---

# ECOSYSTEM 2: USER PROFILE (12 Screens)

## 2.1 Own Profile Screen
**Purpose:** View and edit personal profile
- **Entry Points:** Bottom tab → Profile, Tap avatar
- **Exit Points:**
  - → Profile Edit (tap Edit)
  - → Other Profile (tap own name/link)
  - → Media Gallery (tap grid)
  - → Saved Content (tap bookmark)
  - → Settings (gear icon)
  - → Social Passport (tap passport widget)
- **Components:** Profile header (avatar, cover, name, bio), Stats row, Grid preview, Tab bar (Posts, Saved, Archive), Edit profile button, Settings gear, Story ring (if no stories)
- **Actions:** Edit profile, View stats, Browse media, Access settings
- **Navigation:** Push to edit/settings, Tab switches within screen

## 2.2 Other User Profile Screen
**Purpose:** View another user's public/shared profile
- **Entry Points:** Feed (tap author), Explore (tap user), Chat (tap user)
- **Exit Points:**
  - → Follow/Unfollow (action)
  - → Message (tap button)
  - → Report (tap menu)
  - → Own Profile (tap back)
- **Components:** Profile header, Follow button, Message button, Mutual followers indicator, Bio with link, Social Passport widget, Grid preview, Tab bar (Posts, Stories, About)
- **Actions:** Follow/unfollow, Send message, Report, Block
- **Navigation:** Push to chat, Modal for report

## 2.3 Profile Edit Screen
**Purpose:** Modify profile information
- **Entry Points:** Own Profile (tap Edit)
- **Exit Points:**
  - → Avatar Picker (tap photo)
  - → Cover Picker (tap cover)
  - → Interest Editor (tap interests)
  - → Availability Settings (tap status)
  - → Own Profile (save/back)
- **Components:** Avatar preview, Cover preview, Name input, Username display, Bio textarea, Location picker, Website input, Interest chips, Availability dropdown, Save button, Cancel button
- **Actions:** Edit fields, Pick media, Add interests, Set availability
- **Navigation:** Push to pickers, Modal to availability

## 2.4 Avatar Picker Screen
**Purpose:** Select or capture profile photo
- **Entry Points:** Profile Edit (tap photo)
- **Exit Points:**
  - → Camera (take photo)
  - → Gallery (select existing)
  - → Avatar Crop (select photo)
- **Components:** Camera preview, Gallery button, Recent photos grid, Cancel button
- **Actions:** Take photo, Select from gallery, Cancel
- **Navigation:** Camera capture, Push to crop

## 2.5 Avatar Crop Screen
**Purpose:** Adjust profile photo framing
- **Entry Points:** Avatar Picker (select photo)
- **Exit Points:**
  - → Profile Edit (confirm)
  - → Avatar Picker (retake)
- **Components:** Circular crop frame, Image preview, Zoom slider, Rotate button, Done button, Retake button
- **Actions:** Zoom, Rotate, Confirm, Retake
- **Navigation:** Push to Profile Edit, Pop to Picker

## 2.6 Cover Photo Picker Screen
**Purpose:** Select or capture cover image
- **Entry Points:** Profile Edit (tap cover)
- **Exit Points:**
  - → Camera (take photo)
  - → Gallery (select)
  - → Cover Crop (select photo)
- **Components:** Camera button, Gallery button, Recent photos grid, Remove cover button, Cancel button
- **Actions:** Capture, Select, Remove existing
- **Navigation:** Camera capture, Push to crop

## 2.7 Interest Editor Screen
**Purpose:** Select and manage profile interests
- **Entry Points:** Profile Edit (tap interests)
- **Exit Points:**
  - → Interest Search (search)
  - → Interest Detail (tap interest)
  - → Profile Edit (done)
- **Components:** Search bar, Selected interests (removable), Suggested interests (addable), Popular interests, Category tabs, Done button
- **Actions:** Search, Add, Remove, Browse categories
- **Navigation:** Modal with search, Push to detail

## 2.8 Connections List Screen
**Purpose:** View followers and following
- **Entry Points:** Own Profile (tap followers/following), Other Profile (tap counts)
- **Exit Points:**
  - → User Profile (tap user)
  - → Follow Requests (tap pending)
  - → Own Profile (back)
- **Components:** Segmented control (Followers/Following), User list with avatars/names, Follow back button, Remove button (following), Pending badge, Search bar
- **Actions:** Switch tabs, Search users, Follow/Unfollow, Remove
- **Navigation:** Segmented within screen, Push to profiles

## 2.9 Follow Requests Screen
**Purpose:** Approve/deny follow requests (private accounts)
- **Entry Points:** Connections List (tap pending)
- **Exit Points:**
  - → User Profile (tap user)
  - → Connections List (back)
- **Components:** Request list with avatars, Approve button, Deny button, Time ago, Mutual indicator, Ignore all button
- **Actions:** Approve, Deny, View profile, Ignore all
- **Navigation:** Push to profile, Pop to list

## 2.10 Close Friends List Screen
**Purpose:** Manage close friends circle
- **Entry Points:** Own Profile → Menu → Close Friends
- **Exit Points:**
  - → User Profile (tap user)
  - → Add Close Friend (tap +)
  - → Own Profile (back)
- **Components:** Close friends list, Add button, Remove swipe action, Mutual close friends badge, Empty state
- **Actions:** Add friends, Remove friends, View profiles
- **Navigation:** Push to profile/picker, Pop to profile

## 2.11 Blocked Users Screen
**Purpose:** Manage blocked accounts
- **Entry Points:** Settings → Privacy → Blocked Users
- **Exit Points:**
  - → User Profile (tap user)
  - → Unblock (action)
  - → Settings (back)
- **Components:** Blocked users list, Unblock button, Report indicator, Search bar, Unblock all button
- **Actions:** Unblock users, View profiles, Report, Unblock all
- **Navigation:** Push to profile, Pop to settings

## 2.12 Activity Status Screen
**Purpose:** Set online/availability status
- **Entry Points:** Profile → Status button, Quick toggle
- **Exit Points:**
  - → Status Picker (select)
  - → Custom Status (enter)
  - → Own Profile (done)
- **Components:** Current status display, Status options (Active, Working, Busy, In Meeting, Offline), Custom status input, Duration picker, Clear status button
- **Actions:** Select preset, Enter custom, Set duration, Clear
- **Navigation:** Modal picker, Return to profile

---

# ECOSYSTEM 3: FEED (10 Screens)

## 3.1 Home Feed Screen
**Purpose:** Primary content stream for user
- **Entry Points:** Bottom tab → Home, Push notification
- **Exit Points:**
  - → Post Detail (tap post)
  - → Story View (tap ring)
  - → Reels Tab (tap tab)
  - → Post Creation (tap +)
  - → Profile (tap avatar)
  - → Comments (tap comment icon)
  - → Explore (tap search icon)
- **Components:** Story ring, Post cards (image/video/text), Like button, Comment button, Share button, Save button, More menu, Refresh indicator
- **Actions:** Scroll, Like, Comment, Share, Save, Tap to detail
- **Navigation:** Vertical scroll, Tap to detail, Tab switch

## 3.2 Following Feed Screen
**Purpose:** Content from followed accounts only
- **Entry Points:** Feed → Following tab
- **Exit Points:**
  - → Post Detail (tap post)
  - → User Profile (tap author)
  - → Home Feed (tap For You tab)
- **Components:** Post cards, Following badge, Refresh indicator, Empty state (no follows)
- **Actions:** Scroll, Interact with posts, Switch to For You
- **Navigation:** Vertical scroll, Tap to detail, Tab switch

## 3.3 Near Feed Screen
**Purpose:** Location-filtered content stream
- **Entry Points:** Feed → Near tab, Map → Feed icon
- **Exit Points:**
  - → Post Detail (tap post)
  - → Location Posts (tap location tag)
  - → Map View (tap map icon)
- **Components:** Post cards with location tag, Radius slider, Distance indicator, Map preview
- **Actions:** Scroll, Adjust radius, Tap location
- **Navigation:** Vertical scroll, Push to detail/map

## 3.4 Post Detail Screen
**Purpose:** Full post view with comments
- **Entry Points:** Feed (tap post), Notification (tap)
- **Exit Points:**
  - → Author Profile (tap avatar/name)
  - → Hashtag (tap tag)
  - → Mention (tap @user)
  - → Location (tap place)
  - → Edit Post (author only)
  - → Feed (back/swipe)
- **Components:** Post content, Author header, Action bar, Comments section, Related posts, Share sheet
- **Actions:** Like, Comment, Share, Save, Bookmark, Report
- **Navigation:** Push to profile/detail, Modal for share

## 3.5 Post Creation Screen
**Purpose:** Create new feed post
- **Entry Points:** Home Feed (tap +), Bottom tab → Create
- **Exit Points:**
  - → Camera (take photo/video)
  - → Gallery (select media)
  - → Text Entry (write)
  - → Location Tag (add place)
  - → Tag People (add mentions)
  - → Add Music (search audio)
  - → Post Preview (next)
  - → Discard (back)
- **Components:** Media preview area, Text input, Camera/gallery buttons, Location button, Tag button, Music button, Audience selector, Post button
- **Actions:** Add media, Write caption, Add location, Tag people, Add music
- **Navigation:** Push to preview, Modal to discard confirm

## 3.6 Post Edit Screen
**Purpose:** Modify existing post
- **Entry Points:** Own Post Detail (tap ... → Edit)
- **Exit Points:**
  - → Media Editor (modify media)
  - → Text Edit (modify caption)
  - → Post Detail (save)
  - → Delete Post (action)
- **Components:** Media display, Caption editor, Location editor, Tag editor, Audience selector, Delete button, Save button
- **Actions:** Edit caption, Modify location, Update tags, Delete post
- **Navigation:** Push to detail, Modal for delete confirm

## 3.7 Post Preview Screen
**Purpose:** Review post before publishing
- **Entry Points:** Post Creation (tap Next)
- **Exit Points:**
  - → Home Feed (post)
  - → Post Creation (edit)
  - → Audience Selector (change)
  - → Schedule (schedule)
- **Components:** Preview card, Caption, Tagged users, Location, Audience selector, Schedule toggle, Share to other platforms, Post button
- **Actions:** Preview, Edit, Schedule, Post, Share externally
- **Navigation:** Push to feed (success), Pop to creation

## 3.8 Saved Posts Screen
**Purpose:** View bookmarked content
- **Entry Points:** Own Profile → Saved tab
- **Exit Points:**
  - → Post Detail (tap post)
  - → Collection (tap collection)
  - → Create Collection (tap +)
- **Components:** Saved posts grid, Collection list, Add to collection button, Remove button, Empty state
- **Actions:** View posts, Create collections, Organize saved
- **Navigation:** Vertical scroll, Push to detail/collection

## 3.9 Saved Collection Screen
**Purpose:** Organized saved content folder
- **Entry Points:** Saved Posts (tap collection)
- **Exit Points:**
  - → Post Detail (tap post)
  - → Edit Collection (tap edit)
  - → Saved Posts (back)
- **Components:** Collection header, Posts grid, Post count, Edit button, Remove from collection
- **Actions:** View posts, Reorder, Remove posts, Edit name
- **Navigation:** Push to detail, Pop to list

## 3.10 Scheduled Posts Screen
**Purpose:** View and manage scheduled content
- **Entry Points:** Profile → Menu → Scheduled
- **Exit Points:**
  - → Post Detail (tap scheduled)
  - → Edit Schedule (tap edit)
  - → Post Now (action)
  - → Profile (back)
- **Components:** Scheduled post list, Scheduled time, Edit button, Delete button, Post now button
- **Actions:** Edit timing, Delete, Post immediately, View preview
- **Navigation:** Push to detail, Modal for actions

---

# ECOSYSTEM 4: STORIES (10 Screens)

## 4.1 Stories Bar
**Purpose:** Display and access story ring
- **Entry Points:** Home Feed (top of screen)
- **Exit Points:**
  - → Story Viewer (tap ring)
  - → Add Story (tap + ring)
- **Components:** Your story ring, Friend story rings, Seen indicator, Fresh indicator, Add button
- **Actions:** Tap ring to view, Tap + to create
- **Navigation:** Expand to fullscreen viewer

## 4.2 Story Viewer Screen
**Purpose:** Consume story content
- **Entry Points:** Stories Bar (tap ring), Notification (tap)
- **Exit Points:**
  - → Next Story (swipe/auto-advance)
  - → Previous Story (swipe back)
  - → User Profile (tap name)
  - → Reaction (tap/double-tap)
  - → Reply (swipe up)
  - → Share (tap share)
  - → Home Feed (tap X/background)
- **Components:** Story content (photo/video/text), Progress bar, Username, Timestamp, Reaction picker, Reply box, Share button, More menu
- **Actions:** View content, React, Reply, Share, Navigate between stories
- **Navigation:** Horizontal swipe, Tap to advance, Swipe up to reply

## 4.3 Story Camera Screen
**Purpose:** Capture story content
- **Entry Points:** Stories Bar (tap +), Create button
- **Exit Points:**
  - → Camera Capture (take photo)
  - → Video Capture (record video)
  - → Story Editor (after capture)
  - → Gallery (select)
  - → Cancel
- **Components:** Camera preview, Capture button, Flip camera, Flash toggle, Speed selector, Timer, Focus indicator, Close button
- **Actions:** Take photo, Record video, Flip camera, Adjust flash, Set timer
- **Navigation:** Capture → Push to Editor, Modal for gallery

## 4.4 Story Editor Screen
**Purpose:** Add text, stickers, effects to story
- **Entry Points:** Story Camera (after capture)
- **Exit Points:**
  - → Text Tool (tap T)
  - → Sticker Picker (tap sticker)
  - → Filter Selector (tap filters)
  - → Music Search (tap music)
  - → Draw Tool (tap pen)
  - → Audience Selector (next)
  - → Story Camera (back)
- **Components:** Story preview, Tool bar (text, sticker, filter, music, draw), Undo button, Next button, Discard button
- **Actions:** Add text, Add stickers, Apply filters, Add music, Draw, Undo
- **Navigation:** Bottom toolbar, Push to audience selector

## 4.5 Story Text Editor Screen
**Purpose:** Add styled text to story
- **Entry Points:** Story Editor (tap T)
- **Exit Points:**
  - → Font Picker (change font)
  - → Color Picker (change color)
  - → Background Picker (change bg)
  - → Story Editor (done)
- **Components:** Text input, Font options, Color palette, Alignment options, Background styles, Done button
- **Actions:** Type text, Change font, Change color, Position text
- **Navigation:** Pop to editor

## 4.6 Story Sticker Picker Screen
**Purpose:** Add stickers and GIFs to story
- **Entry Points:** Story Editor (tap sticker)
- **Exit Points:**
  - → Search Stickers (search bar)
  - → Emoji Keyboard (tap emoji tab)
  - → GIPHY (tap GIF tab)
  - → Location Sticker (tap location)
  - → Mention Sticker (tap @)
  - → Poll Sticker (tap poll)
  - → Story Editor (select sticker)
- **Components:** Sticker grid, Search bar, Category tabs, Recent stickers, Trending stickers
- **Actions:** Browse, Search, Select sticker, Add custom
- **Navigation:** Grid selection, Pop to editor

## 4.7 Story Audience Selector Screen
**Purpose:** Choose who sees the story
- **Entry Points:** Story Editor (tap Next)
- **Exit Points:**
  - → Story Posted (share)
  - → Story Editor (back)
  - → Close Friends List (add)
- **Components:** Audience options (Everyone, Close Friends, Specific), Close friends list, Send button, Share options
- **Actions:** Select audience, Add specific people, Post story
- **Navigation:** Push to success/share, Pop to editor

## 4.8 Highlights Screen
**Purpose:** View archived story collections
- **Entry Points:** Profile (below story ring)
- **Exit Points:**
  - → Highlight View (tap highlight)
  - → Create Highlight (tap +)
  - → Story Archive (tap archive)
- **Components:** Highlight covers, Add new button, Archive access, Edit mode
- **Actions:** View highlights, Create new, Edit existing, Delete
- **Navigation:** Push to highlight view, Modal for create

## 4.9 Highlight View Screen
**Purpose:** Watch highlight collection
- **Entry Points:** Highlights (tap cover)
- **Exit Points:**
  - → Story Viewer (tap story)
  - → Edit Highlight (tap edit)
  - → Highlights (back)
- **Components:** Highlight cover, Story list, Title, Edit button, Cover image selector
- **Actions:** Watch stories, Edit title/cover, Add/remove stories
- **Navigation:** Push to viewer, Modal for edit

## 4.10 Create Highlight Screen
**Purpose:** Create new highlight from stories
- **Entry Points:** Highlights (tap +)
- **Exit Points:**
  - → Story Picker (select stories)
  - → Title Entry (enter name)
  - → Cover Picker (select cover)
  - → Highlights (save)
- **Components:** Story selector, Selected stories preview, Title input, Cover preview, Done button
- **Actions:** Select stories, Enter title, Choose cover
- **Navigation:** Push to highlights

## 4.11 Story Archive Screen
**Purpose:** View private story history
- **Entry Points:** Highlights (tap archive)
- **Exit Points:**
  - → Story Detail (tap story)
  - → Restore to Highlights (action)
  - → Highlights (back)
- **Components:** Archived stories list, Date headers, Restore button, Delete button, Empty state
- **Actions:** View stories, Restore to highlight, Delete permanently
- **Navigation:** Vertical scroll, Push to detail

---

# ECOSYSTEM 5: REELS (8 Screens)

## 5.1 Reels Feed Screen
**Purpose:** Full-screen short-form video discovery
- **Entry Points:** Bottom tab → Reels, Feed (tap Reels tab)
- **Exit Points:**
  - → Reel Detail (tap for details)
  - → Creator Profile (tap username)
  - → Sound Page (tap audio)
  - → Comment Sheet (swipe up)
  - → Share Sheet (tap share)
  - → Create Reel (tap +)
  - → Home Feed (swipe tab)
- **Components:** Full-screen video, Creator info, Caption, Sound info, Action bar (like, comment, share, save), Comment sheet, Share sheet
- **Actions:** Scroll (next reel), Like, Comment, Share, Save, Follow creator
- **Navigation:** Vertical scroll, Tap to pause/play, Sheet for comments

## 5.2 Reels Explore Screen
**Purpose:** Discover trending and recommended reels
- **Entry Points:** Reels (tap Explore tab)
- **Exit Points:**
  - → Reel Detail (tap reel)
  - → Hashtag Page (tap #tag)
  - → Creator Profile (tap user)
- **Components:** Reel grid (2 columns), Trending section, Category rows, Search bar
- **Actions:** Browse grid, Tap to watch, Filter by category
- **Navigation:** Grid scroll, Tap to fullscreen

## 5.3 Reels Following Screen
**Purpose:** Reels from followed accounts
- **Entry Points:** Reels (tap Following tab)
- **Exit Points:**
  - → Reel (tap)
  - → Creator Profile (tap user)
- **Components:** Full-screen reels, Following badge, Empty state (no follows with reels)
- **Actions:** Scroll reels, Follow creators
- **Navigation:** Vertical scroll

## 5.4 Reel Creation Screen
**Purpose:** Create new short video
- **Entry Points:** Reels (tap +), Create button
- **Exit Points:**
  - → Camera (record)
  - → Gallery (select)
  - → Template (select)
  - → Effects (select)
  - → Reel Editor (after capture)
- **Components:** Camera preview, Record button, Gallery button, Template gallery, Effects button, Speed control, Timer, Flip camera
- **Actions:** Record video, Select from gallery, Apply effects, Adjust speed
- **Navigation:** Record → Push to editor, Modal for gallery

## 5.5 Reel Editor Screen
**Purpose:** Edit and enhance reel content
- **Entry Points:** Reel Creation (after capture)
- **Exit Points:**
  - → Text Tool (add text)
  - → Sticker Tool (add sticker)
  - → Filter Tool (adjust look)
  - → Audio Editor (edit sound)
  - → Trim Tool (cut video)
  - → Cover Selector (select thumbnail)
  - → Reel Preview (next)
- **Components:** Video preview, Timeline scrubber, Tool bar, Undo/redo, Next button
- **Actions:** Edit video, Add overlays, Adjust audio, Trim
- **Navigation:** Toolbar navigation, Push to preview

## 5.6 Reel Audio Editor Screen
**Purpose:** Add and edit audio for reel
- **Entry Points:** Reel Editor (tap audio)
- **Exit Points:**
  - → Sound Search (search audio)
  - → Original Sound (use own audio)
  - → Sound Trim (adjust timing)
  - → Reel Editor (done)
- **Components:** Sound preview, Search bar, Trending sounds, Sound waveform, Trim handles, Volume sliders (original/music)
- **Actions:** Search sounds, Trim sound, Adjust volume, Select
- **Navigation:** Search modal, Pop to editor

## 5.7 Reel Preview Screen
**Purpose:** Review reel before posting
- **Entry Points:** Reel Editor (tap Next)
- **Exit Points:**
  - → Reels Feed (post)
  - → Share to Feed (option)
  - → Reel Editor (edit)
- **Components:** Full preview, Caption input, Hashtags, Tagged users, Location, Audience selector, Share to feed toggle, Post button
- **Actions:** Preview, Edit caption, Tag people, Add location, Post
- **Navigation:** Push to feed (success), Pop to editor

## 5.8 Reels Creator Studio Screen
**Purpose:** Analytics and management for creators
- **Entry Points:** Profile → Menu → Creator Studio
- **Exit Points:**
  - → Reel Detail (tap reel)
  - → Analytics (view stats)
  - → Monetization (view earnings)
  - → Profile (back)
- **Components:** Total views, Total likes, Follower growth, Top reels, Revenue summary, Content list
- **Actions:** View analytics, Tap reel details, Access monetization
- **Navigation:** Segmented tabs, Push to details

---

# ECOSYSTEM 6: EXPLORE (8 Screens)

## 6.1 Explore Home Screen
**Purpose:** Main discovery and content exploration
- **Entry Points:** Bottom tab → Explore, Search (tap search icon)
- **Exit Points:**
  - → Search Screen (tap search bar)
  - → Trending Topics (tap topic)
  - → Reels (tap reel)
  - → People (tap user)
  - → Hashtag Page (tap #tag)
  - → Location (tap place)
- **Components:** Search bar, Trending section, Category rows, Reels grid, Suggested people, Nearby content, Posts grid
- **Actions:** Search, Browse categories, Tap to view
- **Navigation:** Search modal, Push to detail pages

## 6.2 Trending Topics Screen
**Purpose:** View currently popular topics
- **Entry Points:** Explore (tap Trending section)
- **Exit Points:**
  - → Hashtag Page (tap topic)
  - → Related Topic (tap suggestion)
  - → Explore (back)
- **Components:** Topic list, Post count, Trend indicator, Category filter, Time filter (Today/This Week/This Month)
- **Actions:** Browse trends, Filter by category, Tap topic
- **Navigation:** Vertical scroll, Push to hashtag

## 6.3 Hashtag Page Screen
**Purpose:** View posts with specific hashtag
- **Entry Points:** Explore (tap hashtag), Post (tap tag), Reel (tap tag)
- **Exit Points:**
  - → Post Detail (tap post)
  - → Follow Hashtag (action)
  - → Related Hashtag (tap)
  - → Explore (back)
- **Components:** Hashtag header, Post/reel grid, Follow button, Related hashtags, Post count
- **Actions:** Browse posts, Follow hashtag, Tap related
- **Navigation:** Vertical scroll, Push to detail

## 6.4 People Discovery Screen
**Purpose:** Find and connect with new users
- **Entry Points:** Explore → People tab
- **Exit Points:**
  - → User Profile (tap user)
  - → Search Users (search)
  - → Explore (back)
- **Components:** Suggested users grid, Follow suggestions, Mutual followers, Nearby users, Search bar
- **Actions:** Follow users, Search, Filter (mutual, nearby, popular)
- **Navigation:** Grid scroll, Push to profile

## 6.5 Category Browse Screen
**Purpose:** Explore content by interest category
- **Entry Points:** Explore → Categories
- **Exit Points:**
  - → Subcategory (tap)
  - → Category Content (select category)
  - → Explore (back)
- **Components:** Category grid, Icons, Names, Content count, Featured categories
- **Actions:** Browse categories, Tap category
- **Navigation:** Grid scroll, Push to subcategory

## 6.6 Subcategory Screen
**Purpose:** View content within specific subcategory
- **Entry Points:** Category Browse (tap category)
- **Exit Points:**
  - → Post (tap post)
  - → User (tap creator)
  - → Related Content (tap)
  - → Category (back)
- **Components:** Subcategory header, Content feed, Sort options, Filter options
- **Actions:** Browse content, Filter, Sort
- **Navigation:** Vertical scroll, Push to detail

## 6.7 Search Screen
**Purpose:** Search across all content types
- **Entry Points:** Explore (tap search bar), Any screen (search icon)
- **Exit Points:**
  - → Recent Searches (view)
  - → Suggestions (tap)
  - → Search Results (search)
- **Components:** Search input, Recent searches, Suggestions, Filters, Clear history
- **Actions:** Type query, Select suggestion, Apply filters
- **Navigation:** Inline results, Push to results

## 6.8 Search Results Screen
**Purpose:** Display search results by type
- **Entry Points:** Search (submit query)
- **Exit Points:**
  - → User Profile (tap user)
  - → Post Detail (tap post)
  - → Hashtag Page (tap tag)
  - → Community (tap group)
  - → Event (tap event)
  - → Location (tap place)
- **Components:** Type tabs (All, People, Posts, Tags, Communities, Events, Places), Results list, No results state
- **Actions:** Switch tabs, Tap result, Load more
- **Navigation:** Segmented tabs, Push to detail

---

# ECOSYSTEM 7: MAP (8 Screens)

## 7.1 Full Map Screen
**Purpose:** Interactive map with social activity
- **Entry Points:** Bottom tab → Map, Home (map icon)
- **Exit Points:**
  - → Map Filter (tap filter)
  - → Pin Detail (tap pin)
  - → User Profile (tap avatar)
  - → Event (tap event pin)
  - → Check-in (tap location)
  - → Current Location (tap button)
- **Components:** Map view, Pin markers, Filter chips, Current location button, Search bar, Layer toggle
- **Actions:** Pan/zoom map, Tap pins, Filter layers, Search locations
- **Navigation:** Expand pins to detail, Push to profile/event

## 7.2 Nearby People Screen
**Purpose:** Discover people in your area
- **Entry Points:** Map → People layer, Explore → Nearby People
- **Exit Points:**
  - → User Profile (tap user)
  - → Message (tap message)
  - → Map (back)
- **Components:** User cards with distance, Avatar, Name, Bio preview, Distance indicator, Message button, Map inset
- **Actions:** View users, Tap profile, Send message
- **Navigation:** Vertical scroll, Push to profile, Modal for message

## 7.3 Nearby Events Screen
**Purpose:** Events happening nearby
- **Entry Points:** Map → Events layer, Explore → Events
- **Exit Points:**
  - → Event Detail (tap event)
  - → Map (back)
- **Components:** Event cards, Distance, Date/time, Attendee count, Map inset, Filter button
- **Actions:** Browse events, Filter by time/type, Tap for details
- **Navigation:** Vertical scroll, Push to detail

## 7.4 Nearby Communities Screen
**Purpose:** Groups active in your area
- **Entry Points:** Map → Communities layer, Explore → Communities
- **Exit Points:**
  - → Community Home (tap community)
  - → Map (back)
- **Components:** Community cards, Member count, Activity indicator, Distance, Join button, Map inset
- **Actions:** Browse communities, Join, View on map
- **Navigation:** Vertical scroll, Push to community

## 7.5 Venue Detail Screen
**Purpose:** View place/location information
- **Entry Points:** Map (tap venue pin), Post (tap location)
- **Exit Points:**
  - → Check-in (action)
  - → Events at Venue (tap events)
  - → Posts at Venue (tap posts)
  - → Directions (action)
  - → Map (back)
- **Components:** Venue photo, Name, Address, Rating, Check-in button, Recent posts, Upcoming events, Directions button
- **Actions:** Check-in, View posts, See events, Get directions
- **Navigation:** Vertical scroll, Push to posts/events

## 7.6 Check-in Screen
**Purpose:** Tag current location in content
- **Entry Points:** Venue Detail (tap Check-in), Post Creation (tap location)
- **Exit Points:**
  - → Post Creation (attach check-in)
  - → Search Location (search)
  - → Recent Locations (select)
  - → Venue Detail (tap venue)
- **Components:** Search bar, Recent locations, Popular nearby, Map preview, Confirm button
- **Actions:** Search, Select recent, Confirm
- **Navigation:** Modal return with location

## 7.7 Location Settings Screen
**Purpose:** Control location sharing preferences
- **Entry Points:** Settings → Privacy → Location
- **Exit Points:**
  - → Location Permission (system setting)
  - → Settings (back)
- **Components:** Location permission toggle, Default visibility, Share duration, Block list, Location history
- **Actions:** Toggle settings, Set defaults, View history
- **Navigation:** Modal, Push to system settings

## 7.8 Location History Screen
**Purpose:** View past check-ins and locations
- **Entry Points:** Location Settings (tap History)
- **Exit Points:**
  - → Venue Detail (tap location)
  - → Post (tap post)
  - → Location Settings (back)
- **Components:** Timeline view, Date headers, Location cards, Post previews, Map view toggle, Clear history button
- **Actions:** Browse history, Tap to view, Clear history
- **Navigation:** Vertical scroll, Push to detail

---

# ECOSYSTEM 8: ACTIVITIES (10 Screens)

## 8.1 Events Feed Screen
**Purpose:** Discover and manage events
- **Entry Points:** Bottom tab → Events, Explore → Events
- **Exit Points:**
  - → Event Detail (tap event)
  - → Create Event (tap +)
  - → Filters (tap filter)
  - → Map View (tap map icon)
  - → My Events (tap My Events tab)
- **Components:** Event cards, Filter chips, Tabs (Discover, My Events, Past), Map toggle, Create button
- **Actions:** Browse events, Filter, Create event, View map
- **Navigation:** Vertical scroll, Push to detail, Tab switch

## 8.2 Event Detail Screen
**Purpose:** View complete event information
- **Entry Points:** Events Feed (tap event), Notification (tap)
- **Exit Points:**
  - → RSVP Action (buttons)
  - → Event Chat (tap chat)
  - → Organizer Profile (tap organizer)
  - → Attendee List (tap attendees)
  - → Venue on Map (tap location)
  - → Share Event (share)
  - → Events Feed (back)
- **Components:** Event cover image, Title, Date/time, Location, Description, Organizer info, Attendee preview, RSVP buttons, Share button, Interested button, Save button
- **Actions:** RSVP, Share, Save, Join chat, View attendees, Get directions
- **Navigation:** Vertical scroll, Push to chat/profile, Modal for share

## 8.3 Create Event Screen
**Purpose:** Build and publish new event
- **Entry Points:** Events Feed (tap +), Profile (tap Create Event)
- **Exit Points:**
  - → Cover Photo (upload)
  - → Date/Time Picker (set)
  - → Location Picker (set)
  - → Ticket Setup (add tickets)
  - → Event Preview (preview)
  - → Events Feed (publish)
- **Components:** Title input, Cover upload, Date/time picker, Location picker, Description editor, Category selector, Privacy toggle, Ticket section, Co-host selector
- **Actions:** Fill details, Upload cover, Set date, Set location, Add tickets
- **Navigation:** Push to preview, Success → Feed

## 8.4 Event Date/Time Picker Screen
**Purpose:** Set event timing
- **Entry Points:** Create Event (tap date/time)
- **Exit Points:**
  - → Date Selection (select date)
  - → Time Selection (select time)
  - → Recurring Setup (set repeat)
  - → Create Event (confirm)
- **Components:** Calendar view, Time slots, Duration picker, Timezone display, All day toggle, Recurring options
- **Actions:** Select date, Set time, Choose duration, Set recurrence
- **Navigation:** Date → Time → Return

## 8.5 Event Location Picker Screen
**Purpose:** Select event venue or address
- **Entry Points:** Create Event (tap location)
- **Exit Points:**
  - → Map Search (search)
  - → Venue Picker (select)
  - → Custom Address (enter)
  - → Create Event (confirm)
- **Components:** Map view, Search bar, Recent venues, Suggested venues, Online option, Address input
- **Actions:** Search, Select venue, Enter address, Toggle online
- **Navigation:** Map selection, Modal for custom

## 8.6 Event Ticket Setup Screen
**Purpose:** Configure paid tickets
- **Entry Points:** Create Event (tap Add Tickets)
- **Exit Points:**
  - → Ticket Type Editor (add type)
  - → Attendee Questions (add)
  - → Create Event (confirm)
- **Components:** Ticket types list, Add ticket button, Quantity limits, Price fields, Early bird toggle, Promo code section
- **Actions:** Add ticket types, Set pricing, Add questions, Set limits
- **Navigation:** Modal editor, Return with tickets

## 8.7 Event Preview Screen
**Purpose:** Review event before publishing
- **Entry Points:** Create Event (tap Preview)
- **Exit Points:**
  - → Publish (confirm)
  - → Edit Event (back)
  - → Share (share)
- **Components:** Full event preview, Edit button, Publish button, Share button, Preview as attendee toggle
- **Actions:** Review, Edit details, Publish, Share
- **Navigation:** Push to feed (success), Pop to edit

## 8.8 Event Chat Screen
**Purpose:** Coordinate with attendees
- **Entry Points:** Event Detail (tap Chat), Event (notification)
- **Exit Points:**
  - → Event Detail (tap header)
  - → Attendee Profile (tap user)
  - → Message Thread (tap reply)
  - → Events Feed (back)
- **Components:** Event header, Message list, Date/time reminder, Attendee avatars, Message input, Quick actions
- **Actions:** Send message, View attendees, Tap date reminder
- **Navigation:** Push to profile, Pop to detail

## 8.9 Event Analytics Screen
**Purpose:** View event performance (for organizers)
- **Entry Points:** Event Detail → Menu → Analytics
- **Exit Points:**
  - → Attendee Insights (view details)
  - → Event Detail (back)
- **Components:** Views count, RSVP count, Engagement rate, Traffic sources, Demographics, Growth chart
- **Actions:** View stats, Export data
- **Navigation:** Vertical scroll, Push to insights

## 8.10 My Events Screen
**Purpose:** Manage events user is involved in
- **Entry Points:** Events Feed → My Events tab
- **Exit Points:**
  - → Event Detail (tap event)
  - → Create Event (tap +)
  - → Hosted Events (tab)
  - → Attending Events (tab)
  - → Past Events (tab)
- **Components:** Segmented tabs, Event list, Empty states, Create button
- **Actions:** Switch tabs, Tap event, Create new
- **Navigation:** Segmented tabs, Push to detail

---

# ECOSYSTEM 9: COMMUNITIES (10 Screens)

## 9.1 Communities List Screen
**Purpose:** View joined communities
- **Entry Points:** Bottom tab → Communities, Profile → Communities
- **Exit Points:**
  - → Community Home (tap community)
  - → Discover Communities (tap Explore)
  - → Create Community (tap +)
  - → Notifications (bell icon)
- **Components:** Community cards, Unread indicators, Create button, Search bar, Notification badge
- **Actions:** Browse communities, Search, Create new
- **Navigation:** Push to community, Modal for create

## 9.2 Community Discovery Screen
**Purpose:** Find new communities to join
- **Entry Points:** Communities → Explore tab
- **Exit Points:**
  - → Community Preview (tap community)
  - → Search (search bar)
  - → Category (tap category)
  - → Communities List (back)
- **Components:** Suggested communities, Categories, Trending, Nearby, Search bar
- **Actions:** Browse, Search, Filter by category
- **Navigation:** Vertical scroll, Push to preview

## 9.3 Community Home Screen
**Purpose:** Main community landing page
- **Entry Points:** Communities List (tap community), Explore (tap)
- **Exit Points:**
  - → Community Posts (tab)
  - → Events (tab)
  - → Members (tab)
  - → Settings (gear)
  - → Leave Community (action)
  - → Communities List (back)
- **Components:** Community header (cover, name, description), Tab bar, Post feed, Member preview, Event preview, Join/Leave button, Invite button
- **Actions:** Browse tabs, Join/leave, Invite, Access settings
- **Navigation:** Tab switch within, Push to detail screens

## 9.4 Community Posts Feed Screen
**Purpose:** Content within community
- **Entry Points:** Community Home → Posts tab
- **Exit Points:**
  - → Post Detail (tap post)
  - → Create Post (tap +)
  - → Community Home (back)
- **Components:** Post cards, Create button, Sort options, Community info header
- **Actions:** Scroll posts, Create post, Sort
- **Navigation:** Vertical scroll, Push to detail

## 9.5 Community Channels Screen
**Purpose:** Topic-based sub-groups
- **Entry Points:** Community Home → Channels tab
- **Exit Points:**
  - → Channel View (tap channel)
  - → Create Channel (tap +)
  - → Community Home (back)
- **Components:** Channel list, Unread badges, Channel icons, Description preview, Create button (admin)
- **Actions:** Browse channels, Create channel (admin), View channel
- **Navigation:** Vertical scroll, Push to channel

## 9.6 Channel View Screen
**Purpose:** View discussions in channel
- **Entry Points:** Community Channels (tap channel)
- **Exit Points:**
  - → Post Detail (tap post)
  - → Create Post (tap +)
  - → Community Channels (back)
- **Components:** Channel header, Post feed, Members online, Create button
- **Actions:** Browse posts, Create post, View members
- **Navigation:** Vertical scroll, Push to detail

## 9.7 Community Members Screen
**Purpose:** View and manage members
- **Entry Points:** Community Home → Members tab
- **Exit Points:**
  - → User Profile (tap user)
  - → Role Editor (admin action)
  - → Community Home (back)
- **Components:** Member list, Role badges, Search bar, Filter (admins, mods, members), Invite button, Pending requests
- **Actions:** View members, Change roles (admin), Search, Invite
- **Navigation:** Vertical scroll, Push to profile

## 9.8 Community Events Screen
**Purpose:** Events specific to community
- **Entry Points:** Community Home → Events tab
- **Exit Points:**
  - → Event Detail (tap event)
  - → Create Event (tap +)
  - → Community Home (back)
- **Components:** Upcoming events, Past events, Create button, Attendee preview
- **Actions:** Browse events, Create event, View details
- **Navigation:** Vertical scroll, Push to detail

## 9.9 Community Settings Screen
**Purpose:** Configure community (admins only)
- **Entry Points:** Community Home (gear icon)
- **Exit Points:**
  - → Edit Community (edit info)
  - → Moderation Settings (configure)
  - → Member Management (manage)
  - → Delete Community (danger zone)
  - → Community Home (back)
- **Components:** General settings, Privacy settings, Moderation options, Member management, Danger zone
- **Actions:** Edit settings, Manage members, Delete
- **Navigation:** Push to edit/settings, Modal for delete

## 9.10 Create Community Screen
**Purpose:** Start new community
- **Entry Points:** Communities (tap +)
- **Exit Points:**
  - → Cover Photo (upload)
  - → Category Picker (select)
  - → Privacy Selector (choose)
  - → Community Preview (preview)
  - → Communities List (publish)
- **Components:** Name input, Description, Cover upload, Category picker, Privacy toggle, Rules editor, Icon selector
- **Actions:** Fill details, Set privacy, Add rules
- **Navigation:** Push to preview, Success → community

---

# ECOSYSTEM 10: CHATS (12 Screens)

## 10.1 Chats List Screen
**Purpose:** View all conversations
- **Entry Points:** Bottom tab → Inbox, Notification (tap)
- **Exit Points:**
  - → Chat Thread (tap conversation)
  - → New Message (tap +)
  - → Calls List (tap calls tab)
  - → Archived Chats (tap archive)
  - → Spam/Junk (tap menu)
- **Components:** Chat list, Unread badges, Typing indicator, Mute indicator, Pin indicator, Search bar
- **Actions:** Tap chat, Search chats, Archive, Mute, Pin
- **Navigation:** Push to thread, Modal for new message

## 10.2 Chat Thread Screen
**Purpose:** Real-time messaging
- **Entry Points:** Chats List (tap conversation)
- **Exit Points:**
  - → User Profile (tap avatar)
  - → Media Gallery (tap media)
  - → Message Options (tap message)
  - → Call (tap call button)
  - → Chats List (back)
- **Components:** Message bubbles, Date dividers, Media previews, Typing indicator, Input bar, Call button, Media button, Reaction picker
- **Actions:** Send message, Send media, React, Reply, Call
- **Navigation:** Push to profile/media, Pop to list

## 10.3 New Message Screen
**Purpose:** Start new conversation
- **Entry Points:** Chats List (tap +)
- **Exit Points:**
  - → User Select (select recipient)
  - → Group Setup (create group)
  - → Chat Thread (start conversation)
- **Components:** Recipient selector, Recent chats, Contacts list, Search bar, Create group button
- **Actions:** Select recipient, Create group, Start chat
- **Navigation:** Push to thread

## 10.4 Group Setup Screen
**Purpose:** Configure group chat
- **Entry Points:** New Message (tap Create Group)
- **Exit Points:**
  - → Add Members (select)
  - → Name Entry (set name)
  - → Avatar Picker (set photo)
  - → Chat Thread (create)
- **Components:** Member selector, Group name input, Avatar picker, Create button
- **Actions:** Add members, Set name, Set avatar
- **Navigation:** Push to thread

## 10.5 Media Gallery Screen
**Purpose:** View shared media in chat
- **Entry Points:** Chat Thread (tap media button)
- **Exit Points:**
  - → Media Detail (tap media)
  - → Chat Thread (back)
- **Components:** Media grid, Date headers, Video indicators, Photo count
- **Actions:** Browse media, Tap to view, Filter by type
- **Navigation:** Grid scroll, Push to detail

## 10.6 Media Detail Screen
**Purpose:** View full media item
- **Entry Points:** Media Gallery (tap item)
- **Exit Points:**
  - → Save Media (action)
  - → Share Media (action)
  - → Media Gallery (swipe)
  - → Chat Thread (back)
- **Components:** Full-screen media, Sender info, Timestamp, Save button, Share button, Forward button
- **Actions:** View, Save, Share, Forward
- **Navigation:** Swipe for next/prev, Pop to gallery

## 10.7 Message Options Screen
**Purpose:** Actions for specific message
- **Entry Points:** Chat Thread (long-press message)
- **Exit Points:**
  - → Reply (action)
  - → Copy (action)
  - → Forward (action)
  - → Delete (action)
  - → React (select emoji)
  - → Chat Thread (dismiss)
- **Components:** Action list, Reaction picker, Delete warning
- **Actions:** Reply, Copy, Forward, Delete, React
- **Navigation:** Modal return, Action execution

## 10.8 Call Screen (Active)
**Purpose:** Voice or video call interface
- **Entry Points:** Chat Thread (tap call), User Profile (tap call)
- **Exit Points:**
  - → End Call (action)
  - → Flip Camera (action)
  - → Mute/Unmute (action)
  - → Speaker (action)
  - → Chat Thread (end call)
- **Components:** Video preview (video call), Avatar display, Timer, Control bar (mute, speaker, end, flip)
- **Actions:** Mute, Unmute, Speaker toggle, End call, Flip camera
- **Navigation:** Return to chat on end

## 10.9 Calls List Screen
**Purpose:** View call history
- **Entry Points:** Chats → Calls tab
- **Exit Points:**
  - → Call Screen (tap call)
  - → User Profile (tap user)
  - → Chats List (back)
- **Components:** Call history list, Call type icons (voice/video), Duration, Status (missed/answered), Callback button
- **Actions:** View history, Tap to call back, View profile
- **Navigation:** Push to call/profile

## 10.10 Chat Settings Screen
**Purpose:** Configure chat or group
- **Entry Points:** Chat Thread (tap header)
- **Exit Points:**
  - → Member List (view)
  - → Add Member (action)
  - → Media Gallery (view)
  - → Search Messages (search)
  - → Notifications (configure)
  - → Chat Thread (back)
- **Components:** Chat info, Member list preview, Media preview, Settings options, Notifications toggle, Search
- **Actions:** Manage members, View media, Search, Configure notifications
- **Navigation:** Push to detail screens

## 10.11 Archived Chats Screen
**Purpose:** View archived conversations
- **Entry Points:** Chats List (tap Archive)
- **Exit Points:**
  - → Chat Thread (tap)
  - → Unarchive (action)
  - → Chats List (back)
- **Components:** Archived chat list, Unarchive button, Search bar
- **Actions:** View archived, Unarchive, Search
- **Navigation:** Push to thread, Swipe to unarchive

## 10.12 Chat Search Screen
**Purpose:** Search within conversation
- **Entry Points:** Chat Settings (tap Search)
- **Exit Points:**
  - → Message Highlight (tap result)
  - → Chat Thread (back)
- **Components:** Search input, Date filter, Results list, Highlight on match
- **Actions:** Search messages, Tap to jump
- **Navigation:** Scroll to message

---

# ECOSYSTEM 11: NOTIFICATIONS (6 Screens)

## 11.1 Notification Center Screen
**Purpose:** View all activity notifications
- **Entry Points:** Bottom tab → Activity, App icon badge
- **Exit Points:**
  - → Content Detail (tap notification)
  - → Mark All Read (action)
  - → Settings (gear icon)
  - → Filter (tap filter)
- **Components:** Notification list, Type icons, Time stamps, Mark read, Filter chips, Empty state
- **Actions:** View notifications, Mark as read, Filter by type
- **Navigation:** Push to content, Modal to settings

## 11.2 Notification Settings Screen
**Purpose:** Configure notification preferences
- **Entry Points:** Notification Center (gear), Settings → Notifications
- **Exit Points:**
  - → Category Settings (tap category)
  - → Quiet Hours (set)
  - → Settings (back)
- **Components:** Category toggles, Sound selector, Badge style, Quiet hours, Preview
- **Actions:** Toggle categories, Set quiet hours, Choose sounds
- **Navigation:** Push to category, Modal for quiet hours

## 11.3 Notification Category Settings Screen
**Purpose:** Detailed category configuration
- **Entry Points:** Notification Settings (tap category)
- **Exit Points:**
  - → Notification Settings (back)
- **Components:** Category header, Push toggle, Email toggle, In-app toggle, Frequency selector, Sound selector
- **Actions:** Configure each channel, Set frequency
- **Navigation:** Pop to settings

## 11.4 Quiet Hours Screen
**Purpose:** Set do-not-disturb schedule
- **Entry Points:** Notification Settings (tap Quiet Hours)
- **Exit Points:**
  - → Enable/Disable (toggle)
  - → Time Picker (set times)
  - → Notification Settings (back)
- **Components:** Enable toggle, Start time, End time, Days selector, Override option
- **Actions:** Enable, Set times, Select days
- **Navigation:** Modal return

## 11.5 Notification Detail Screen
**Purpose:** View single notification content
- **Entry Points:** Notification Center (tap)
- **Exit Points:**
  - → Related Content (action)
  - → Notification Center (back)
- **Components:** Notification content, Action buttons, Related preview
- **Actions:** View content, Take action
- **Navigation:** Push to content

## 11.6 Archived Notifications Screen
**Purpose:** View dismissed notifications
- **Entry Points:** Notification Center → Menu → Archive
- **Exit Points:**
  - → Notification (tap)
  - → Notification Center (back)
- **Components:** Archived notification list, Restore button, Clear all button
- **Actions:** View archived, Restore, Clear
- **Navigation:** Push to notification, Pop to center

---

# ECOSYSTEM 12: SEARCH (6 Screens)

## 12.1 Search Home Screen
**Purpose:** Entry point for all search
- **Entry Points:** Header (search icon), Explore → Search tab
- **Exit Points:**
  - → Search Input (start typing)
  - → Recent Searches (tap)
  - → Suggestions (tap)
  - → Search Results (submit)
- **Components:** Search input, Recent searches, Trending, Suggested hashtags, Voice search button
- **Actions:** Type, Use voice, Tap suggestion
- **Navigation:** Inline expand, Push to results

## 12.2 Search Input Screen
**Purpose:** Active search interface
- **Entry Points:** Search Home (tap input)
- **Exit Points:**
  - → Search Results (submit)
  - → Filter Sheet (tap filter)
  - → Recent (tap)
  - → Search Home (cancel)
- **Components:** Search input, Clear button, Cancel button, Filter button, Recent searches
- **Actions:** Type query, Clear, Cancel, Apply filters
- **Navigation:** Push to results, Modal for filters

## 12.3 Search Results Overview Screen
**Purpose:** Display all results by type
- **Entry Points:** Search (submit)
- **Exit Points:**
  - → People (tap)
  - → Posts (tap)
  - → Hashtags (tap)
  - → Communities (tap)
  - → Events (tap)
  - → Places (tap)
- **Components:** Type tabs, Results list, No results state, Search term display
- **Actions:** Switch tabs, Tap results, Load more
- **Navigation:** Tab switch, Push to detail

## 12.4 People Search Results Screen
**Purpose:** User search results
- **Entry Points:** Search Results → People tab
- **Exit Points:**
  - → User Profile (tap user)
  - → Search Results (back)
- **Components:** User cards, Mutual indicator, Follow button, Filter button
- **Actions:** View profiles, Follow, Filter
- **Navigation:** Push to profile

## 12.5 Content Search Results Screen
**Purpose:** Post and reel search results
- **Entry Points:** Search Results → Posts tab
- **Exit Points:**
  - → Post Detail (tap post)
  - → User Profile (tap author)
  - → Search Results (back)
- **Components:** Post cards, Sort options, Date filter, Load more
- **Actions:** View posts, Sort, Filter, Load more
- **Navigation:** Push to detail

## 12.6 Search Filters Screen
**Purpose:** Apply search refinements
- **Entry Points:** Search Input (tap filter)
- **Exit Points:**
  - → Apply Filters (confirm)
  - → Clear Filters (action)
  - → Search Input (cancel)
- **Components:** Filter options, Date range, Location range, Media type, Sort order
- **Actions:** Select filters, Apply, Clear
- **Navigation:** Modal return with filters

---

# ECOSYSTEM 13: SOCIAL PASSPORT (8 Screens)

## 13.1 Passport Overview Screen
**Purpose:** View complete social passport
- **Entry Points:** Profile (tap passport widget), Tab → Passport
- **Exit Points:**
  - → Score Breakdown (tap score)
  - → Achievements (tap badges)
  - → Stats Detail (tap stat)
  - → Profile (back)
- **Components:** Passport card, Score gauge, Achievement badges, Stats grid, Share button, Timeline preview
- **Actions:** View score, Tap achievements, Share passport
- **Navigation:** Push to breakdowns, Modal for share

## 13.2 Score Breakdown Screen
**Purpose:** Detailed passport score analysis
- **Entry Points:** Passport Overview (tap score)
- **Exit Points:**
  - → Component Detail (tap component)
  - → Passport Overview (back)
- **Components:** Score gauge, Category breakdown, Contribution chart, Historical trend
- **Actions:** View breakdown, Tap components
- **Navigation:** Vertical scroll, Push to detail

## 13.3 Component Detail Screen
**Purpose:** Deep dive into score component
- **Entry Points:** Score Breakdown (tap component)
- **Exit Points:**
  - → Related Activity (tap item)
  - → Score Breakdown (back)
- **Components:** Component score, Activity list, Tips to improve, Related actions
- **Actions:** View activities, Take suggested actions
- **Navigation:** Vertical scroll, Push to activity

## 13.4 Achievements Screen
**Purpose:** View all earned badges
- **Entry Points:** Passport Overview → Achievements tab
- **Exit Points:**
  - → Achievement Detail (tap badge)
  - → Passport Overview (back)
- **Components:** Badge grid, Earned badges, Locked badges, Category filter, Progress bars
- **Actions:** View badges, Check progress, Filter by category
- **Navigation:** Grid scroll, Push to detail

## 13.5 Achievement Detail Screen
**Purpose:** View specific achievement
- **Entry Points:** Achievements (tap badge)
- **Exit Points:**
  - → Share Achievement (action)
  - → Related Action (action)
  - → Achievements (back)
- **Components:** Badge display, Description, Requirements, Progress, Reward, Share button
- **Actions:** View details, Share, Take action
- **Navigation:** Pop to list

## 13.6 Passport Stats Screen
**Purpose:** Detailed statistics view
- **Entry Points:** Passport Overview → Stats tab
- **Exit Points:**
  - → Activity Detail (tap item)
  - → Passport Overview (back)
- **Components:** Stat cards, Charts, Time period selector, Export button
- **Actions:** Browse stats, Change time period, Export
- **Navigation:** Vertical scroll, Push to detail

## 13.7 Passport Share Screen
**Purpose:** Share passport publicly
- **Entry Points:** Passport Overview (tap Share)
- **Exit Points:**
  - → Share Sheet (share)
  - → Passport Overview (cancel)
- **Components:** Preview card, Privacy selector, Share options, Copy link
- **Actions:** Choose privacy, Share
- **Navigation:** Modal share sheet

## 13.8 Passport History Screen
**Purpose:** View passport changes over time
- **Entry Points:** Passport Overview → History tab
- **Exit Points:**
  - → Activity (tap event)
  - → Passport Overview (back)
- **Components:** Timeline, Score changes, Activity log, Milestones
- **Actions:** Browse history, Tap activity
- **Navigation:** Vertical scroll, Push to activity

---

# ECOSYSTEM 14: REPUTATION (6 Screens)

## 14.1 Trust Profile Screen
**Purpose:** View visible reputation summary
- **Entry Points:** Profile → Trust tab, Settings → Reputation
- **Exit Points:**
  - → Reviews Received (view)
  - → Trust Settings (edit)
  - → Profile (back)
- **Components:** Trust score, Badge display, Recent reviews preview, Verification status
- **Actions:** View reviews, Adjust visibility, Verify identity
- **Navigation:** Push to reviews, Modal to settings

## 14.2 Reviews Received Screen
**Purpose:** View feedback from others
- **Entry Points:** Trust Profile (tap Reviews)
- **Exit Points:**
  - → Review Detail (tap review)
  - → Write Review (action)
  - → Trust Profile (back)
- **Components:** Review list, Rating breakdown, Filter by type, Sort options
- **Actions:** Browse reviews, Filter, Sort
- **Navigation:** Vertical scroll, Push to detail

## 14.3 Review Detail Screen
**Purpose:** View single review
- **Entry Points:** Reviews Received (tap review)
- **Exit Points:**
  - → User Profile (tap reviewer)
  - → Report Review (action)
  - → Reviews Received (back)
- **Components:** Review content, Reviewer info, Rating categories, Response section
- **Actions:** View details, Report, Respond
- **Navigation:** Pop to list

## 14.4 Write Review Screen
**Purpose:** Leave feedback for interaction
- **Entry Points:** Post-event prompt, User Profile (tap Review)
- **Exit Points:**
  - → Star Rating (select)
  - → Category Ratings (select)
  - → Write Review (submit)
- **Components:** Star selector, Category ratings, Text input, Submit button
- **Actions:** Rate, Write feedback, Submit
- **Navigation:** Modal return

## 14.5 Verification Center Screen
**Purpose:** Manage identity verification
- **Entry Points:** Trust Profile (tap Verify), Settings → Verification
- **Exit Points:**
  - → ID Verification (start)
  - → Phone Verification (start)
  - → Email Verification (start)
  - → Trust Profile (back)
- **Components:** Verification options, Status badges, Instructions, Benefits display
- **Actions:** Start verification, View status
- **Navigation:** Push to verification flow

## 14.6 Incident History Screen
**Purpose:** View past safety incidents
- **Entry Points:** Trust Profile → Incidents, Settings → Safety
- **Exit Points:**
  - → Incident Detail (tap)
  - → Appeal (action)
  - → Trust Profile (back)
- **Components:** Incident list, Status badges, Appeal button, Resolution info
- **Actions:** View incidents, Appeal decisions
- **Navigation:** Vertical scroll, Push to detail

---

# ECOSYSTEM 15: PREMIUM (8 Screens)

## 15.1 Premium Home Screen
**Purpose:** Overview of premium offerings
- **Entry Points:** Profile → Premium, Settings → Premium
- **Exit Points:**
  - → Upgrade Options (view plans)
  - → Feature Details (tap feature)
  - → Current Plan (view)
  - → Profile (back)
- **Components:** Current plan badge, Feature highlights, Plan comparison, Upgrade button
- **Actions:** View features, Compare plans, Upgrade
- **Navigation:** Push to upgrade, Modal for details

## 15.2 Upgrade Plans Screen
**Purpose:** Select subscription tier
- **Entry Points:** Premium Home (tap Upgrade)
- **Exit Points:**
  - → Plan Detail (tap tier)
  - → Checkout (select plan)
  - → Premium Home (back)
- **Components:** Plan cards (Free, Plus, Pro, Business), Feature comparison, Price display, Toggle (monthly/yearly)
- **Actions:** Compare plans, Select plan
- **Navigation:** Push to checkout

## 15.3 Plan Comparison Screen
**Purpose:** Detailed feature comparison
- **Entry Points:** Upgrade Plans (tap "Compare All")
- **Exit Points:**
  - → Upgrade Plans (back)
- **Components:** Comparison table, Checkmarks, Feature descriptions, Recommended badge
- **Actions:** Browse comparison, Select plan
- **Navigation:** Pop to plans

## 15.4 Checkout Screen
**Purpose:** Complete purchase
- **Entry Points:** Upgrade Plans (select plan)
- **Exit Points:**
  - → Payment Method (select)
  - → Order Summary (view)
  - → Success (complete)
  - → Cancel
- **Components:** Plan summary, Price breakdown, Payment method selector, Promo code input, Subscribe button
- **Actions:** Select payment, Apply promo, Subscribe
- **Navigation:** Push to success, Modal for payment

## 15.5 Payment Method Screen
**Purpose:** Add/select payment
- **Entry Points:** Checkout (tap payment)
- **Exit Points:**
  - → Add Card (action)
  - → Apple Pay / Google Pay (select)
  - → Checkout (confirm)
- **Components:** Saved cards, Add new card, Payment apps, Default selector
- **Actions:** Add card, Select method
- **Navigation:** Modal for add card, Return to checkout

## 15.6 Subscription Management Screen
**Purpose:** View and manage active subscription
- **Entry Points:** Premium Home → Current Plan
- **Exit Points:**
  - → Change Plan (action)
  - → Cancel Subscription (action)
  - → Billing History (view)
  - → Premium Home (back)
- **Components:** Current plan, Renewal date, Change button, Cancel button, Billing history link
- **Actions:** Change plan, Cancel, View billing
- **Navigation:** Push to change/cancel

## 15.7 Cancel Subscription Screen
**Purpose:** Cancel and capture feedback
- **Entry Points:** Subscription Management (tap Cancel)
- **Exit Points:**
  - → Downgrade (confirm)
  - → Keep Subscription (dismiss)
  - → Subscription Management (back)
- **Components:** Plan retention offers, Feedback form, Final confirmation, Keep button
- **Actions:** Accept offer, Cancel, Provide feedback
- **Navigation:** Modal result

## 15.8 Billing History Screen
**Purpose:** View past payments
- **Entry Points:** Subscription Management (tap History)
- **Exit Points:**
  - → Invoice Detail (tap)
  - → Update Payment (action)
  - → Subscription Management (back)
- **Components:** Invoice list, Amount, Date, Status, Download buttons
- **Actions:** View invoices, Download, Update payment
- **Navigation:** Vertical scroll, Push to invoice

---

# ECOSYSTEM 16: SAFETY (8 Screens)

## 16.1 Safety Check Screen
**Purpose:** Quick safety status overview
- **Entry Points:** Profile → Menu → Safety, Settings → Safety
- **Exit Points:**
  - → Blocked Users (manage)
  - → Privacy Settings (configure)
  - → Two-Factor (enable)
  - → Profile (back)
- **Components:** Safety score, Quick actions, Recent alerts, Tips
- **Actions:** View status, Take action, Configure
- **Navigation:** Push to detail screens

## 16.2 Safety Settings Screen
**Purpose:** Comprehensive safety controls
- **Entry Points:** Safety Check (gear icon), Settings → Privacy & Safety
- **Exit Points:**
  - → Message Controls (configure)
  - → Story Controls (configure)
  - → Tag Controls (configure)
  - → Activity Status Controls (configure)
  - → Safety Check (back)
- **Components:** Category toggles, Control options, Info cards, Status indicators
- **Actions:** Configure controls, View info
- **Navigation:** Push to detailed settings

## 16.3 Message Controls Screen
**Purpose:** Control who can message you
- **Entry Points:** Safety Settings (tap Messages)
- **Exit Points:**
  - → Allow List (manage)
  - → Message Controls (back)
- **Components:** Toggle switches, Description text, Allow list preview, Exception options
- **Actions:** Toggle settings, Manage allow list
- **Navigation:** Push to allow list

## 16.4 Blocked Users Management Screen
**Purpose:** Manage blocked accounts
- **Entry Points:** Safety Check (tap Blocked), Settings → Blocked Users
- **Exit Points:**
  - → Unblock User (action)
  - → User Profile (tap user)
  - → Block New (search)
  - → Safety Check (back)
- **Components:** Blocked list, Search to block, Unblock buttons
- **Actions:** Unblock, Block new, View profiles
- **Navigation:** Vertical scroll, Push to profile

## 16.5 Report Flow Screen
**Purpose:** Submit content/user report
- **Entry Points:** Any content (tap report)
- **Exit Points:**
  - → Issue Type Selection (select)
  - → Details Entry (enter info)
  - → Evidence Upload (add)
  - → Confirmation (submit)
- **Components:** Issue categories, Description input, Screenshot option, Submit button
- **Actions:** Select type, Add details, Submit
- **Navigation:** Step-by-step wizard

## 16.6 Report Confirmation Screen
**Purpose:** Confirm report submission
- **Entry Points:** Report Flow (submit)
- **Exit Points:**
  - → Report Another (action)
  - → Home (close)
- **Components:** Confirmation message, Report ID, Next steps, Close button
- **Actions:** Report another, Close
- **Navigation:** Modal dismiss

## 16.7 Emergency Contacts Screen
**Purpose:** Manage trusted contacts
- **Entry Points:** Safety Check → Emergency Contacts
- **Exit Points:**
  - → Add Contact (action)
  - → Contact Detail (tap)
  - → Safety Check (back)
- **Components:** Contact list, Add button, Permission toggles, Instructions
- **Actions:** Add contact, Set permissions, View contact
- **Navigation:** Push to add/view

## 16.8 Crisis Resources Screen
**Purpose:** Access help and support
- **Entry Points:** Safety Check → Get Help, Report Flow → Resources
- **Exit Points:**
  - → Call Hotline (action)
  - → Crisis Chat (action)
  - → External Resources (browse)
- **Components:** Hotlines list, Chat options, Resource categories, Search
- **Actions:** Call, Chat, Browse resources
- **Navigation:** Deep links to external

---

# ECOSYSTEM 17: MODERATION (6 Screens)

## 17.1 Mod Queue Screen
**Purpose:** Review reported content
- **Entry Points:** Admin Dashboard → Queue, Community → Mod Tools
- **Exit Points:**
  - → Content Review (tap item)
  - → Filter Options (apply)
  - → Admin Dashboard (back)
- **Components:** Queue list, Type filters, Priority badges, Age indicators
- **Actions:** Review items, Filter queue, Prioritize
- **Navigation:** Vertical scroll, Push to review

## 17.2 Content Review Screen
**Purpose:** Evaluate reported content
- **Entry Points:** Mod Queue (tap item)
- **Exit Points:**
  - → Take Action (select)
  - → Escalate (action)
  - → Mod Queue (back)
- **Components:** Content display, Context info, Reporter info, Action buttons, Notes field
- **Actions:** Review, Take action, Add notes, Escalate
- **Navigation:** Pop to queue

## 17.3 Mod Action Confirmation Screen
**Purpose:** Confirm moderation action
- **Entry Points:** Content Review (select action)
- **Exit Points:**
  - → Confirm (execute)
  - → Content Review (back)
- **Components:** Action summary, User notification preview, Confirm button, Cancel button
- **Actions:** Confirm action, Cancel
- **Navigation:** Modal return

## 17.4 Appeals Queue Screen
**Purpose:** Review user appeals
- **Entry Points:** Admin Dashboard → Appeals
- **Exit Points:**
  - → Appeal Review (tap)
  - → Policy Reference (view)
  - → Admin Dashboard (back)
- **Components:** Appeal list, Status badges, Priority indicators, Appeal reason
- **Actions:** Review appeals, View policy
- **Navigation:** Vertical scroll, Push to review

## 17.5 Appeal Review Screen
**Purpose:** Evaluate user appeal
- **Entry Points:** Appeals Queue (tap appeal)
- **Exit Points:**
  - → Original Decision (view)
  - → Policy (view)
  - → Take Action (select)
  - → Appeals Queue (back)
- **Components:** Appeal text, Original action, User history, Action buttons, Notes
- **Actions:** Review, Uphold/Reverse, Add notes
- **Navigation:** Pop to queue

## 17.6 Moderation Log Screen
**Purpose:** View moderation history
- **Entry Points:** Admin Dashboard → Logs, Community → Mod Tools
- **Exit Points:**
  - → Action Detail (tap)
  - → Filter (apply)
  - → Admin Dashboard (back)
- **Components:** Log entries, Date filters, Action type filters, User filters, Export
- **Actions:** Browse logs, Filter, Export
- **Navigation:** Vertical scroll, Push to detail

---

# ECOSYSTEM 18: ANALYTICS (6 Screens)

## 18.1 Personal Stats Screen
**Purpose:** View own activity statistics
- **Entry Points:** Profile → Stats, Settings → Stats
- **Exit Points:**
  - → Stat Detail (tap)
  - → Time Period (select)
  - → Profile (back)
- **Components:** Stat cards, Charts, Time period selector, Export button
- **Actions:** View stats, Change time period, Export
- **Navigation:** Vertical scroll, Push to detail

## 18.2 Creator Studio Dashboard Screen
**Purpose:** Main analytics hub for creators
- **Entry Points:** Profile → Creator Studio
- **Exit Points:**
  - → Content Performance (tap)
  - → Audience Insights (tap)
  - → Revenue (tap)
  - → Profile (back)
- **Components:** Overview cards, Quick links, Chart previews, Notification alerts
- **Actions:** Navigate sections, View summaries
- **Navigation:** Push to detail sections

## 18.3 Content Performance Screen
**Purpose:** Detailed content analytics
- **Entry Points:** Creator Studio (tap Content)
- **Exit Points:**
  - → Post Detail (tap)
  - → Content Performance (back)
- **Components:** Top posts list, Performance chart, Engagement breakdown, Export
- **Actions:** View performance, Compare content, Export
- **Navigation:** Vertical scroll, Push to detail

## 18.4 Audience Insights Screen
**Purpose:** Demographics and behavior
- **Entry Points:** Creator Studio (tap Audience)
- **Exit Points:**
  - → Audience Detail (tap)
  - → Audience Insights (back)
- **Components:** Demographics cards, Growth chart, Peak times, Top locations
- **Actions:** View demographics, Analyze growth
- **Navigation:** Vertical scroll

## 18.5 Revenue Dashboard Screen
**Purpose:** Earnings and monetization
- **Entry Points:** Creator Studio (tap Revenue)
- **Exit Points:**
  - → Transaction Detail (tap)
  - → Payout Settings (action)
  - → Creator Studio (back)
- **Components:** Earnings summary, Chart, Transaction list, Payout button
- **Actions:** View earnings, Request payout, View transactions
- **Navigation:** Vertical scroll, Push to details

## 18.6 Admin Dashboard Screen
**Purpose:** Platform-wide analytics
- **Entry Points:** Admin Portal → Dashboard
- **Exit Points:**
  - → Detailed Reports (navigate)
  - → User Management (navigate)
  - → Content Oversight (navigate)
- **Components:** KPI cards, Platform charts, Alerts, Navigation links
- **Actions:** Monitor metrics, Drill down, Access tools
- **Navigation:** Push to detail sections

---

# ECOSYSTEM 19: SETTINGS (10 Screens)

## 19.1 Settings Hub Screen
**Purpose:** Central settings navigation
- **Entry Points:** Profile → Menu → Settings, Any screen (gear icon)
- **Exit Points:**
  - → Account Settings (navigate)
  - → Privacy Settings (navigate)
  - → Notification Settings (navigate)
  - → Security Settings (navigate)
  - → Accessibility (navigate)
  - → Help Center (navigate)
  - → About (navigate)
- **Components:** Settings categories, Current user info, App version, Support link
- **Actions:** Navigate categories, Search settings
- **Navigation:** Push to detail categories

## 19.2 Account Settings Screen
**Purpose:** Manage account details
- **Entry Points:** Settings Hub → Account
- **Exit Points:**
  - → Edit Name (edit)
  - → Change Username (edit)
  - → Change Email (edit)
  - → Change Phone (edit)
  - → Change Password (edit)
  - → Delete Account (action)
  - → Settings Hub (back)
- **Components:** Account info fields, Edit buttons, Verification status, Danger zone
- **Actions:** Edit details, Delete account
- **Navigation:** Push to edit, Modal for delete

## 19.3 Privacy Settings Screen
**Purpose:** Control privacy across app
- **Entry Points:** Settings Hub → Privacy
- **Exit Points:**
  - → Profile Privacy (configure)
  - → Activity Status (configure)
  - → Location Privacy (configure)
  - → Data & History (view)
  - → Settings Hub (back)
- **Components:** Privacy toggles, Info cards, Data links
- **Actions:** Configure privacy, View data
- **Navigation:** Push to detailed settings

## 19.4 Accessibility Settings Screen
**Purpose:** Accessibility accommodations
- **Entry Points:** Settings Hub → Accessibility
- **Exit Points:**
  - → Display Settings (configure)
  - → Motion Settings (configure)
  - → Voice Settings (configure)
  - → Settings Hub (back)
- **Components:** Toggle switches, Sliders, Descriptions, Preview
- **Actions:** Configure accessibility, Preview changes
- **Navigation:** Push to detailed settings

## 19.5 Language Settings Screen
**Purpose:** App language configuration
- **Entry Points:** Settings Hub → Language
- **Exit Points:**
  - → Select Language (choose)
  - → Content Language (configure)
  - → Settings Hub (back)
- **Components:** Language list, Current selection, Region variants, Content language option
- **Actions:** Select language, Configure content language
- **Navigation:** Push to selection, Return

## 19.6 Data Settings Screen
**Purpose:** Data management and export
- **Entry Points:** Settings Hub → Data
- **Exit Points:**
  - → Download Data (action)
  - → Clear Cache (action)
  - → Usage Stats (view)
  - → Settings Hub (back)
- **Components:** Download button, Cache size, Usage stats, Storage breakdown
- **Actions:** Download data, Clear cache, View usage
- **Navigation:** Push to download, Action modals

## 19.7 Help Center Screen
**Purpose:** Self-service support
- **Entry Points:** Settings Hub → Help
- **Exit Points:**
  - → Article List (browse)
  - → Search Help (search)
  - → Contact Us (action)
  - → Settings Hub (back)
- **Components:** Search bar, Category list, Recent articles, Contact button
- **Actions:** Search, Browse, Contact support
- **Navigation:** Push to articles, Modal to contact

## 19.8 Help Article Screen
**Purpose:** View help article
- **Entry Points:** Help Center (tap article)
- **Exit Points:**
  - → Related Article (tap)
  - → Contact Support (action)
  - → Help Center (back)
- **Components:** Article content, Screenshots, Related articles, Helpful rating
- **Actions:** Read, Rate helpful, Contact
- **Navigation:** Vertical scroll, Push to related

## 19.9 About Screen
**Purpose:** App information and legal
- **Entry Points:** Settings Hub → About
- **Exit Points:**
  - → Privacy Policy (view)
  - → Terms of Service (view)
  - → Licenses (view)
  - → Updates (check)
  - → Settings Hub (back)
- **Components:** App info, Version, Legal links, Update button, Social links
- **Actions:** View legal, Check updates
- **Navigation:** Push to webview, Deep link to store

## 19.10 Delete Account Screen
**Purpose:** Permanently remove account
- **Entry Points:** Account Settings → Delete Account
- **Exit Points:**
  - → Download Data (first step)
  - → Confirm Deletion (action)
  - → Account Settings (cancel)
- **Components:** Warning message, Data download link, Confirmation checkbox, Delete button
- **Actions:** Download data, Confirm, Delete
- **Navigation:** Step-by-step flow

---

# ECOSYSTEM 20: ADMINISTRATION (8 Screens)

## 20.1 Admin Dashboard Screen
**Purpose:** Platform operations overview
- **Entry Points:** Admin Portal (login)
- **Exit Points:**
  - → User Management (navigate)
  - → Content Oversight (navigate)
  - → Trust & Safety (navigate)
  - → Analytics (navigate)
  - → Support Queue (navigate)
- **Components:** KPI cards, Alerts, Quick actions, Navigation sidebar
- **Actions:** Monitor platform, Navigate tools
- **Navigation:** Push to detail sections

## 20.2 User Management Screen
**Purpose:** Search and manage users
- **Entry Points:** Admin Dashboard → Users
- **Exit Points:**
  - → User Detail (tap user)
  - → Search Filters (apply)
  - → Admin Dashboard (back)
- **Components:** Search bar, User list, Filter options, Bulk action toolbar
- **Actions:** Search users, Filter, Bulk actions
- **Navigation:** Vertical scroll, Push to detail

## 20.3 User Detail Screen
**Purpose:** Comprehensive user view
- **Entry Points:** User Management (tap user)
- **Exit Points:**
  - → Account Actions (take)
  - → Content List (view)
  - → Moderation History (view)
  - → User Management (back)
- **Components:** User profile, Account status, Action buttons, Activity timeline, Associated accounts
- **Actions:** Take actions, View content, View history
- **Navigation:** Push to actions, Tab within screen

## 20.4 Account Actions Screen
**Purpose:** Execute admin actions
- **Entry Points:** User Detail (tap action)
- **Exit Points:**
  - → Confirm Action (confirm)
  - → User Detail (cancel)
- **Components:** Action selector, Reason input, Duration selector, Evidence upload, Notify user toggle
- **Actions:** Select action, Submit
- **Navigation:** Modal return

## 20.5 Content Oversight Screen
**Purpose:** Platform-wide content search
- **Entry Points:** Admin Dashboard → Content
- **Exit Points:**
  - → Content Detail (tap)
  - → Filter Panel (apply)
  - → Admin Dashboard (back)
- **Components:** Search bar, Filters, Content list, Type selector, Status badges
- **Actions:** Search, Filter, View content
- **Navigation:** Vertical scroll, Push to detail

## 20.6 Trust & Safety Dashboard Screen
**Purpose:** Safety metrics and incidents
- **Entry Points:** Admin Dashboard → Safety
- **Exit Points:**
  - → Incident Detail (tap)
  - → Trend Analysis (view)
  - → Escalations (view)
  - → Admin Dashboard (back)
- **Components:** Safety metrics, Incident list, Trend charts, Escalation queue
- **Actions:** Monitor safety, Investigate, Escalate
- **Navigation:** Push to detail, Tab within screen

## 20.7 Support Queue Screen
**Purpose:** User support tickets
- **Entry Points:** Admin Dashboard → Support
- **Exit Points:**
  - → Ticket Detail (tap)
  - → Assign Ticket (action)
  - → Admin Dashboard (back)
- **Components:** Ticket list, Priority badges, Status filters, Assignee field
- **Actions:** View tickets, Assign, Resolve
- **Navigation:** Vertical scroll, Push to detail

## 20.8 Support Ticket Detail Screen
**Purpose:** Handle support case
- **Entry Points:** Support Queue (tap ticket)
- **Exit Points:**
  - → User Profile (view)
  - → Take Action (execute)
  - → Reply (send)
  - → Support Queue (back)
- **Components:** Ticket content, User info, Conversation thread, Action buttons, Internal notes
- **Actions:** Reply, Escalate, Resolve, Add notes
- **Navigation:** Pop to queue

---

# SCREEN COUNT SUMMARY

| Ecosystem | Screen Count |
|-----------|-------------|
| 1. Authentication | 15 |
| 2. User Profile | 12 |
| 3. Feed | 10 |
| 4. Stories | 11 |
| 5. Reels | 8 |
| 6. Explore | 8 |
| 7. Map | 8 |
| 8. Activities | 10 |
| 9. Communities | 10 |
| 10. Chats | 12 |
| 11. Notifications | 6 |
| 12. Search | 6 |
| 13. Social Passport | 8 |
| 14. Reputation | 6 |
| 15. Premium | 8 |
| 16. Safety | 8 |
| 17. Moderation | 6 |
| 18. Analytics | 6 |
| 19. Settings | 10 |
| 20. Administration | 8 |
| **TOTAL** | **156** |

---

# NAVIGATION MATRIX

## Primary Navigation Flows

```
BOTTOM TAB BAR
├── Home (Feed)
│   ├── Stories → Story Viewer
│   ├── Posts → Post Detail
│   └── Create Post → Post Preview
│
├── Explore
│   ├── Search → Results
│   ├── Trending → Hashtag
│   ├── Categories → Subcategory
│   └── People → User Profile
│
├── Create (+)
│   ├── Post → Preview → Feed
│   ├── Story → Editor → Post
│   ├── Reel → Editor → Preview → Feed
│   └── Event → Preview → Events
│
├── Inbox (Chats)
│   ├── Chat Thread → Profile / Call
│   ├── New Message → Group Setup
│   └── Calls → Call Screen
│
└── Profile
    ├── Edit Profile
    ├── Social Passport
    ├── Settings
    └── Premium
```

## Cross-Ecosystem Navigation

```
STORY RING → ANY PROFILE
FEED → USER PROFILE
CHAT → USER PROFILE
EVENT → ORGANIZER PROFILE
COMMUNITY → MEMBER PROFILES
MAP → USER PROFILES
NOTIFICATION → CONTENT/PROFILE
SEARCH → USER/PROFILE/CONTENT
PREMIUM → PROFILE (Badge)
SAFETY → PROFILE (Blocking)
```

---

# DOCUMENT CONTROL

- **Version:** 1.0
- **Date:** June 2026
- **Author:** Chief UX Architect
- **Status:** Information Architecture Complete

---

*This document defines the complete screen inventory for LinkUp, suitable for design system development, product planning, and engineering implementation.*

*Total Screens: 156 (within target range of 120-200)*