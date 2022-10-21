# Inbox Application

## User Interface
![image](https://user-images.githubusercontent.com/946070/197158091-c71775f7-0408-44fc-a3b1-a919c0de113a.png)

## High Level Architecture
[High Level Architecture](https://app.diagrams.net/#G1mOMlQIR4K0D9l8fUITVno7_zHTdKj5wt?mode=github)
These are the high level components break down of the Inbox application
 
- Inbox Application
  + Inbox UI
      - Inbox Contacts List
      - Inbox Message Area
      - Inbox UserInfo
  + Inbox Storage/Cache
    - Inbox Messages Storage
      - Inbox Media Storage
  + Inbox Communication Engine
    - Inbox REST API
    - Inbox WebSocket API
    - Inbox Media Storage API
    - Inbox Push Message Handler API
  + Inbox Logger
  + Inbox Telemetry

![image](https://user-images.githubusercontent.com/946070/197159652-deabbbd1-eeb1-47b9-ad79-9770a825df3c.png)

## API
These are the high level APIs
- REST APIs
  + [getUserInfo(userId)](getUserInfo(userId))
  + [getMessageInfo(messageId)](getMessageInfo(messageId))
  + [addAssignee(messageId, userId)](addAssignee(messageId, userId))
  + [changeStatus(messageId, status)](changeStatus(messageId, status))
  + [updateInfo(userId, basicInformation)](updateInfo(userId, basicInformation))
  + [updateInfo(userId, buisnessInformation)](updateInfo(userId, buisnessInformation))
  + [updateInfo(userId, notes)](updateInfo(userId, notes))
- WebSocket APIs
- Media Storage APIs
- Push Message Handler APIs

### REST APIs
#### <a name="getUserInfo(userId)"></a>getUserInfo(userId)
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


#### <a name="getMessageInfo(messageId)"></a>getMessageInfo(messageId)
Request
```
HTTP GET /message/{messageId}
```

Response
```javascript
{
    messageId: string
    assignedTo: string;
    userId: string;
    userName: string;
    assigneeName: string;
    status: string;

}
```

#### <a name="addAssignee(messageId, userId)"></a>addAssignee(messageId, userId)
Request
```
HTTP POST /message/{messageId}/{userId}
```

Response
```javascript
{
    messageId: string
    assignedTo: string;
    userId: string;
    userName: string;
    assigneeName: string;
    status: string;
}
```


#### <a name="changeStatus(messageId, status)"></a>changeStatus(messageId, status)
Request
```
HTTP POST /message/{messageId}
```

Request Data
``` javascript
{
    status: string;
}
```

Response
```javascript
{
    messageId: string
    assignedTo: string;
    userId: string;
    userName: string;
    assigneeName: string;
    status: string;
}
```

#### <a name="updateInfo(userId, basicInformation)"></a>updateInfo(userId, basicInformation)
Request
```
HTTP PATCH /user/{messageId}
```

Request Data
``` javascript
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

#### <a name="updateInfo(userId, buisnessInformation)"></a>updateInfo(userId, buisnessInformation)
Request
```
HTTP PATCH /user/{messageId}
```

Request Data
``` javascript
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

#### <a name="updateInfo(userId, notes)"></a>updateInfo(userId, notes)
Request
```
HTTP PATCH /user/{messageId}
```

Request Data
``` javascript
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


## Data Flow
