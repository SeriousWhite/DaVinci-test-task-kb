# Knowledge Base

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
    id: 1216,
    sprintVelocity: 13,
  },
  {
    id: 1226,
    sprintVelocity: 9,
  },
];
```

- GET /api/statistic/velocity/sprint?id=id

```javascript
{
    "id": 1216,
    "sprintVelocity": 13
}
```

2. Issue lead time:

- GET /api/statistic/leadTime/allIssues

```javascript
[
  {
    id: 98333,
    leadTime: 1,
  },
  {
    id: 96473,
    leadTime: 332,
  },
];
```

- GET /api/statistic/leadTime/issue?id=id

```javascript
{
    "id": 96473,
    "leadTime": 332
}
```

3. Issue development lead time:

- GET /api/statistic/developmentLeadTime/allIssues

```javascript
[
  {
    id: 98333,
    developmentLeadTime: 1,
  },
  {
    id: 96473,
    developmentLeadTime: 11,
  },
];
```

- GET /api/statistic/developmentLeadTime/issue?id=id

```javascript
{
    "id": 96473,
    "developmentLeadTime": 11
}
```

4. Issue testing lead time:

- GET /api/statistic/testingLeadTime/allIssues

```javascript
[
  {
    id: 98333,
    testingLeadTime: 0,
  },
  {
    id: 96473,
    testingLeadTime: 321,
  },
];
```

- GET /api/statistic/testingLeadTime/issue?id=id

```javascript
{
    "id": 96473,
    "testingLeadTime": 321
}
```

5. Stabilization ratio:

- GET /api/statistic/stabilizationRatio/issue?id=id

```javascript
{
    "id": 96465,
    "stabilizationRatio": 2
}
```

6. Development hours/story points:

- GET /api/statistic/developmentDividedByPoints/issue?id=id

```javascript
{
    "id": 96465,
    "developmentDividedByPoints": 0.2
}
```

#### Additional endpoints:

1. All sprints:

- GET /api/allSprints

```javascript
[
  {
    id: 1212,
    name: "0.7.0: fe0.11.1_be0.4.5",
    createdOn: "2020-03-16T06:15:44Z",
    projectName: "Micro Distributing E05G3",
    status: "open",
  },
  {
    id: 1216,
    name: "0.9.0: fe0.12.1_be0.5.9",
    createdOn: "2020-03-26T09:12:19Z",
    projectName: "Micro Distributing E05G3",
    status: "open",
  },
];
```

2. All issues:

- GET /api/allIssues

```javascript
[
  {
    id: 98341,
    projectName: "Micro Distributing E05G3",
    trackerName: "[scrum] User Story",
    statusName: "Closed",
    priorityName: "Medium",
    authorName: "Andreyev Ilya",
    targetVersionName: "0.9.0: fe0.12.1_be0.5.9",
    subject: "Tesst task",
    storyPoint: "11",
    createdOn: "2021-02-18T17:37:14Z",
  },
  {
    id: 98337,
    projectName: "Micro Distributing E05G3",
    trackerName: "[scrum] User Story",
    statusName: "Closed",
    priorityName: "Medium",
    authorName: "Andreyev Ilya",
    targetVersionName: "1. 0.11.0:fe0.18.3_be0.9.1",
    subject: "styled-components",
    storyPoint: "9",
    createdOn: "2021-02-17T22:08:00Z",
  },
];
```
