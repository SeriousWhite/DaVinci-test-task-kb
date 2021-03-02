# Knowledge Base

## Links

Environment url: https://davinci-test-task-frontend.herokuapp.com

Demo url: [link](https://syberry-my.sharepoint.com/personal/i_andreyev_syberry_com/_layouts/15/onedrive.aspx?id=%2Fpersonal%2Fi%5Fandreyev%5Fsyberry%5Fcom%2FDocuments%2F2021%2D03%2D02%2017%2D24%2D19%2Emkv&parent=%2Fpersonal%2Fi%5Fandreyev%5Fsyberry%5Fcom%2FDocuments&originalPath=aHR0cHM6Ly9zeWJlcnJ5LW15LnNoYXJlcG9pbnQuY29tLzp2Oi9wL2lfYW5kcmV5ZXYvRVl1RWk2eWZxYk5Na3NTd0ZLRmhQTUVCT0V3Z2Zuc0RZQjdYR0VLcUxXX2o4UT9ydGltZT1PR0xaMEpYZDJFZw)

## Decomposition of the implementation

1. Backend enviroment setup using "Express.js". (1h)
2. Making all the necessary requests to the Redmine API using "axios" package to get all the values for calculating metrics such as "sprint velocity", "issue lead time", "issue development lead time", "issue testing lead time", "stabilization ratio", "development hours/story points". (12h)
3. Processing data received from Redmine API. (12h)
4. Endpoints implementation. (4h)
5. Frontend enviroment setup using "React.js". (1h)
6. Disable CORS for my Frontend origin on Backend using "cors" package. (0.5h)
7. Making requests to the my Backend using "axios". (4h)
8. Processing data received from my Backend. (8h)
9. Layout using styled-components, data implementation from my Backend using "react-table" or "recharts". (14h)

Optimistic estimate time: 50h
Most likely estimate time: 60h
Pessimistic estimate time: 70h

## Design implementation

### Api Design

#### Main endpoints:

1. Sprint velocity:

- GET /api/statistic/velocity/allSprints

```javascript
[
  {
    id: "1236",
    velocity: "10",
    sprintName: "1. 0.15.0:fe0.22.0_be0.18.3",
  },
  {
    id: "1220",
    velocity: "4",
    sprintName: "0.9.0-fix: fe0.12.1_be0.5.17",
  },
];
```

- GET /api/statistic/velocity/sprint?id=id

```javascript
{
    "id": "1216",
    "velocity": "2",
}
```

2. Issue lead time:

- GET /api/statistic/leadTime/allIssues

```javascript
[
  {
    id: "98342",
    sprintName: "1. 0.15.0:fe0.22.0_be0.18.3",
    issueAssignedTo: "Andreyev Ilya",
    leadTime: "3",
    developmentLeadTime: "2",
    testingLeadTime: "1",
  },
  {
    id: "96463",
    sprintName: "1. 0.15.2: fe0.22.8_be_0.18.11",
    issueAssignedTo: "Admin QARedmine",
    leadTime: "342",
    developmentLeadTime: "3",
    testingLeadTime: "339",
  },
];
```

- GET /api/statistic/leadTime/issue?id=id

```javascript
{
    "id": "96473",
    "leadTime": "332",
}
```

3. Issue development lead time:

- GET /api/statistic/developmentLeadTime/issue?id=id

```javascript
{
    "id": "96473",
    "developmentLeadTime": "11",
}
```

4. Issue testing lead time:

- GET /api/statistic/testingLeadTime/issue?id=id

```javascript
{
    "id": "96473",
    "testingLeadTime": "321",
}
```

5. Stabilization ratio:

- GET /api/statistic/stabilizationRatio/issue?id=id

```javascript
{
    "id": "96465",
    "stabilizationRatio": "2",
}
```

6. Development hours/story points:

- GET /api/statistic/productivity/issue?id=id

```javascript
{
    "id": "96465",
    "productivity": "0.2",
}
```

#### Additional endpoints:

1. All sprints:

- GET /api/allSprints

```javascript
[
  {
    id: "1216",
    name: "0.9.0: fe0.12.1_be0.5.9",
    createdOn: "2020-03-26T09:12:19Z",
    projectName: "Micro Distributing E05G3",
    status: "closed",
  },
  {
    id: "1220",
    name: "0.9.0-fix: fe0.12.1_be0.5.17",
    createdOn: "2020-03-30T17:14:37Z",
    projectName: "Micro Distributing E05G3",
    status: "closed",
  },
];
```

2. All issues:

- GET /api/allIssues

```javascript
[
  {
    id: "98342",
    projectName: "Micro Distributing E05G3",
    trackerName: "[scrum] User Story",
    statusName: "Closed",
    priorityName: "Medium",
    authorName: "Andreyev Ilya",
    targetVersionName: "1. 0.15.0:fe0.22.0_be0.18.3",
    subject: "Internal Communications",
    storyPoint: "10",
    createdOn: "2021-02-18T19:22:16Z",
  },
  {
    id: "96463",
    projectName: "Micro Distributing E05G3",
    trackerName: "[scrum] User Story",
    statusName: "Closed",
    priorityName: "Medium",
    authorName: "Admin QARedmine",
    targetVersionName: "1. 0.15.2: fe0.22.8_be_0.18.11",
    subject: "My Profile",
    storyPoint: "6",
    createdOn: "2020-03-06T15:03:39Z",
  },
];
```
