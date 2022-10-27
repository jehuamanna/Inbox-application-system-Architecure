# Inbox Application


- [Inbox Application](#inbox-application)
  * [User Interface](#user-interface)
  * [High Level Architecture](#high-level-architecture)
  * [API](#api)
  * [UI Components](#ui-components)
    + [High Level UI Components](#high-level-ui-components)
      - [InboxChatUI](#inboxchatui)
      - [InboxChatUserListWithMessages](#inboxchatuserlistwithmessages)
      - [InboxChatConversationListWithMessages](#inboxchatconversationlistwithmessages)
      - [InboxChatUserInformation](#inboxchatuserinformation)
    + [Sub Components](#sub-components)
      - [SearchAndFilter](#searchandfilter)
      - [UserListCard](#userlistcard)
      - [ConversationMessageCard](#conversationmessagecard)
      - [ApplicationStatusCard](#applicationstatuscard)
      - [Tabs](#tabs)
      - [BasicUserInformationCard](#basicuserinformationcard)
      - [BuisnessUserInformationCard](#buisnessuserinformationcard)
      - [InputAndAttachmentsPanel](#inputandattachmentspanel)
  * [Data Models](#data-models)
  * [Data Flow](#data-flow)
  * [Tech Stack](#tech-stack)
  * [Top metrics to measure success](#top-metrics-to-measure-success)
  * [Reliability and extensiblity considerations](#reliability-and-extensiblity-considerations)
  * [Other Points To Discuss](#other-points-to-discuss)
  * [API Details](#api-details)
    + [<a name="getUserInfo(userId)"></a>getUserInfo(userId)](#-a-name--getuserinfo-userid-----a-getuserinfo-userid-)
    + [<a name="getMessageInfo(messageId)"></a>getMessageInfo(messageId)](#-a-name--getmessageinfo-messageid-----a-getmessageinfo-messageid-)
    + [<a name="addAssignee(messageIduserId)"></a>addAssignee(messageId, userId)](#-a-name--addassignee-messageiduserid-----a-addassignee-messageid--userid-)
    + [<a name="changeStatus(messageIdstatus)"></a>changeStatus(messageId, status)](#-a-name--changestatus-messageidstatus-----a-changestatus-messageid--status-)
    + [<a name="updateInfo(userIdbasicInformation)"></a>updateInfo(userId, basicInformation)](#-a-name--updateinfo-useridbasicinformation-----a-updateinfo-userid--basicinformation-)
    + [<a name="updateInfo(userIdbuisnessInformation)"></a>updateInfo(userId, buisnessInformation)](#-a-name--updateinfo-useridbuisnessinformation-----a-updateinfo-userid--buisnessinformation-)
    + [<a name="updateInfo(userIdnotes)"></a>updateInfo(userId, notes)](#-a-name--updateinfo-useridnotes-----a-updateinfo-userid--notes-)





## User Interface

![image](https://user-images.githubusercontent.com/946070/197158091-c71775f7-0408-44fc-a3b1-a919c0de113a.png)

## High Level Architecture

[Logical Architecture](https://app.diagrams.net/#G1mOMlQIR4K0D9l8fUITVno7_zHTdKj5wt?mode=github)

![image](https://user-images.githubusercontent.com/946070/197348524-3d002c3f-12cd-44c8-94be-7f990294cda1.png)

[High Level Architecture](https://app.diagrams.net/#G1xK5Xg6QbL8vFGZZhMI-nzAjsJiU_AKs1?mode=github)

![image](https://user-images.githubusercontent.com/946070/197348507-5f8ef4c4-d79d-4934-b494-67249d28f089.png)

These are the high level components break down of the Inbox application

- Inbox UI
  - Inbox Contacts List
  - Inbox Message Area
  - Inbox UserInfo
- Inbox Storage/Cache
  - Inbox Messages Storage
    - Inbox Media Storage
- Inbox Communication Engine
  - Inbox REST API
  - Inbox WebSocket API
  - Inbox Media Storage API
  - Inbox Push Message Handler API
- Inbox Logger
- Inbox Telemetry
- Inbox Data Encryption

## API

- These are the high level APIs

  - [getUserInfo(userId)](<#getUserInfo(userId)>)
  - [getMessageInfo(messageId)](<#getMessageInfo(messageId)>)
  - [addAssignee(messageId, userId)](<#addAssignee(messageIduserId)>)
  - [changeStatus(messageId, status)](<#changeStatus(messageIdstatus)>)
  - [updateInfo(userId, basicInformation)](<#updateInfo(userIdbasicInformation)>)
  - [updateInfo(userId, buisnessInformation)](<#updateInfo(userIdbuisnessInformation)>)
  - [updateInfo(userId, notes)](<#updateInfo(userIdnotes)>)
  - fetchMessages()
    - filter
    - search
  - receiveNewMessage(userId)
  - sendNewMessage(userId)



## UI Components

- ### High Level UI Components

  - #### InboxChatUI

    InboxChatUI component launchs a fully functional Inbox application. All the UI Components are interlinked and work together to launch a fully functional application.

    ```jsx
    import { InboxChatUI } from "./components/InboxChat";

    export default function App(props) {
      return (
        <div style={{ width: "800px", height: "800px" }}>
          <InboxChatUI />
        </div>
      );
    }
    ```

  - #### InboxChatUserListWithMessages

    The InboxChatUserListWithMessages is a component with a list of users. The component has all the necessary listeners and methods required to display the user's list and shows the set of the messages/chats of the selected user.

    ```jsx
    import { InboxChatUserListWithMessages } from "./components/InboxChat";

    export default function App(props) {
      return (
        <div style={{ width: "800px", height: "800px" }}>
          <InboxChatUserListWithMessages chatWithUser={props.userId} />
        </div>
      );
    }
    ```

  - #### InboxChatConversationListWithMessages

    The InboxChatConversationListWithMessages is a component with a list of recent conversations. The component has all the necessary listeners and methods required to display the recent conversation list and shows the set of the messages/chats of the selected recent conversation.

    ```jsx
    import { InboxChatConversationListWithMessages } from "./components/InboxChat";

    export default function App(props) {
      return (
        <div style={{ width: "800px", height: "800px" }}>
          <InboxChatConversationListWithMessages />
        </div>
      );
    }
    ```

  - #### InboxChatUserInformation

    The InboxChatUserInformation is a component that shows all personal and buisness profile information along with notes.

    ```jsx
    import { InboxChatUserInformation } from "./components/InboxChat";

    export default function App(props) {
      return (
        <div style={{ width: "800px", height: "800px" }}>
          <InboxChatUserInformation userId={userId} />
        </div>
      );
    }
    ```

- ### Sub Components

  - #### SearchAndFilter
  - #### UserListCard
  - #### ConversationMessageCard
  - #### ApplicationStatusCard
  - #### Tabs
  - #### BasicUserInformationCard
  - #### BuisnessUserInformationCard
  - #### InputAndAttachmentsPanel

- Component Driven Design.

  We need to build an entire set of components broken down to atomic level.

  - Atoms
  - Molecules
  - Organisms
  - Templates
  - Pages

  Check out [this](https://bradfrost.com/blog/post/atomic-web-design/) article for more details.

## Data Models

- IMessageList

```typescript
interface IMessageList {
  userName: string;
  message: IMessage[];
  status: StatusType;
  assignedTo: string;
}
```

- IMessage

```typescript
interface IMessage {
  timestamp: string;
  messageType: string;
  data: string;
}
```

- IApplicationStatus

```typescript
interface IApplicationStatus {
  assignedTo: string;
  userName: string;
  status: StatusType;
}
```

- IUserInfo

```typescript
interface IUserInfo {
  basicInformation: {
    userName: string;
    emailAddress: string;
    phoneNumber: string;
  };
  buisnessInformation: {
    buisnessName: string;
    name: string;
    emailAddress: string;
    buisnessId: number;
    lastOrder: string;
    totalOrders: number;
    totalSpent: string;
  };
  notes: string;
}
```

- StatusType

```typescript
type StatusType = 'open' | 'in-progress' | 'closed'
}
```

## Data Flow

[Network Data Flow](https://app.diagrams.net/#G1sM_yEV7b5UbC5Xb3xozTMtbEUPixigyg)


![image](https://user-images.githubusercontent.com/946070/197406680-0e336bc3-4a31-4595-b583-d36800fe5446.png)


[Application Data Flow](https://app.diagrams.net/#G1mkNYjomi1XNnZlVv0DwIQP26AzHT4qs0)



![image](https://user-images.githubusercontent.com/946070/198301028-cfe6d174-dcf1-47f5-af88-d11c0f76e876.png)


## Tech Stack

- Rendering Library.
  - React.
- State Management.
  - xState.
- Module Bundlers.
  - esbuild
- Type checking tools.
  - TypeScript.
- Transpilers.
  - TypeScript compiler.
- Unit Testing frameworks.
  - Jest.
- Integration Testing frameworks.
  - Playwright.
- Telemetry(erros and API calls).
  - Datadog/Sentry.
- Analytics.
  - Google Analytics/Cloudfare.

## Top metrics to measure success

- Number of minutes active user
- No of transactions per user.
- No of clicks on the UserListCards.
- Success/Failure messages.
- Code coverage.
- Unit testing.
- Integration testing.
- Accessibility w3c complaint.
- Development velocity.
- Loading time.
- Time taken to send/recieve messages.

## Reliability and extensiblity considerations

- Success/Failure messages.
- Retry mechanisms
- Data protection of stored messages.
- Adding support for a new messaging system.
- Handling failure scenarios
- Adding additional properties for messages to be copied, liked, deleted.



## Other Points To Discuss
- Performance and Optimization
    1. Network.
        1. Code splitting
            1. chat code,
            2. caching
            3. Loading images faster.
            4. Vendor code.
            5. ES6 code.
            6. minify resources
        2. Gzip.
        3. HTTP/2

    2. JavaScript.
        1. Do less stuff.
        2. Minify the shipping code.
        3. Ship less polyfill

    3. Rendering.
        1. Inline Critical Resources.
        2. Load analytics scripts later.
        3. Show shimmer/skeleton for user experience.
        4. Load noncritical JS in deferred mode.
        5. Use a constant number of nodes while showing the list.

    4. Images, Video, Audio, PDF
        1. Compression,
        2. CDN

    5. Caching.
        1. Chat messages.
        2. Images, Videos, PDFs, 
        3. CSS


- Accessibility.
    1. Keyboard Events.
    2. Touch events.
    3. Color Themes.
    4. Voice commands for live events.
    5. Force REM units instead of pixels.
    6. Hotkeys.
    7. Alt Attributes.
    8. Semantic HTML
- Network
  1. Long polling.
  2. WebSockets.
  3. SSE.

## API Details
- ### <a name="getUserInfo(userId)"></a>getUserInfo(userId)
  Request

```
HTTP GET /user/{userId}
```

Response

```javascript
{
    userId: string;
    basicInformation: {
        emailAddress: string;
        phoneNumber: string;
    },
    buisnessInformation: {
        buisnessName: string;
        name: string;
        emailAddress: string;
        buisnessId: number;
        lastOrder: string;
        totalOrders: number;
        totalSpent: string;
    },
    notes: string;
}
```

- ### <a name="getMessageInfo(messageId)"></a>getMessageInfo(messageId)
  Request

```
HTTP GET /message/{messageId}
```

Response

```javascript
{
  messageId: string;
  assignedTo: string;
  userId: string;
  userName: string;
  assigneeName: string;
  status: string;
}
```

- ### <a name="addAssignee(messageIduserId)"></a>addAssignee(messageId, userId)
  Request

```
HTTP POST /message/{messageId}/{userId}
```

Response

```javascript
{
  messageId: string;
  assignedTo: string;
  userId: string;
  userName: string;
  assigneeName: string;
  status: string;
}
```

- ### <a name="changeStatus(messageIdstatus)"></a>changeStatus(messageId, status)
  Request

```
HTTP POST /message/{messageId}
```

Request Data

```javascript
{
  status: string;
}
```

Response

```javascript
{
  messageId: string;
  assignedTo: string;
  userId: string;
  userName: string;
  assigneeName: string;
  status: string;
}
```

- ### <a name="updateInfo(userIdbasicInformation)"></a>updateInfo(userId, basicInformation)
  Request

```
HTTP PATCH /user/{messageId}
```

Request Data

```javascript
{
    basicInformation: {
        emailAddress: string;
        phoneNumber: string;
    },
}
```

Response

```javascript
{
    userId: string;
    basicInformation: {
        emailAddress: string;
        phoneNumber: string;
    },
    buisnessInformation: {
        buisnessName: string;
        name: string;
        emailAddress: string;
        buisnessId: number;
        lastOrder: string;
        totalOrders: number;
        totalSpent: string;
    },
    notes: string;
}
```

- ### <a name="updateInfo(userIdbuisnessInformation)"></a>updateInfo(userId, buisnessInformation)
  Request

```
HTTP PATCH /user/{messageId}
```

Request Data

```javascript
{
    buisnessInformation: {
        buisnessName: string;
        name: string;
        emailAddress: string;
        buisnessId: number;
        lastOrder: string;
        totalOrders: number;
        totalSpent: string;
    },
}
```

Response

```javascript
{
    userId: string;
    basicInformation: {
        emailAddress: string;
        phoneNumber: string;
    },
    buisnessInformation: {
        buisnessName: string;
        name: string;
        emailAddress: string;
        buisnessId: number;
        lastOrder: string;
        totalOrders: number;
        totalSpent: string;
    },
    notes: string;
}
```

- ### <a name="updateInfo(userIdnotes)"></a>updateInfo(userId, notes)
  Request

```
HTTP PATCH /user/{messageId}
```

Request Data

```javascript
{
  notes: string;
}
```

Response

```javascript
{
    userId: string;
    basicInformation: {
        emailAddress: string;
        phoneNumber: string;
    },
    buisnessInformation: {
        buisnessName: string;
        name: string;
        emailAddress: string;
        buisnessId: number;
        lastOrder: string;
        totalOrders: number;
        totalSpent: string;
    },
    notes: string;
}
```
