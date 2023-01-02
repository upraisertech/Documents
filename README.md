---
title: Connecting from React Apps
---

import useBaseUrl from '@docusaurus/useBaseUrl';
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

In this section you'll learn how to connect to your Stackprint API from [React](https://reactjs.org) apps with generated client code. The shown code examples are based on generated client code for an API deployed from the default API configuration and the **Note** resource. For your API and object types, the names of services, functions and parameters will likely be different.

A full example React application that connects to a Stackprint API can be found on [GitHub](https://github.com/stackprint/example-notes-react).

## Setup

- On your [Stackprint Dashboard](https://console.stackprint.io) click **Generate client code** under your API and select **React (TypeScript)** to generate React client code for that API and download it
- Extract the downloaded archive to **<react_project_folder>/src/gen/typescript-axios-client**
- Install axios:

<Tabs
defaultValue="npm"
values={[
{label: 'npm', value: 'npm'},
{label:'yarn', value: 'yarn'},
]}>
<TabItem value="npm">

```bash
npm install --save axios
```

</TabItem>
<TabItem value="yarn">

```bash
yarn add axios
```

</TabItem>
</Tabs>

- Import and instantiate a service to connect to your resource from any component:

```typescript
...
import { NoteApi, Note } from "../gen/typescript-axios-client";

const Notes = () => {
  ...
  const loadNotes = async () => {
    const noteApi = new NoteApi({});
    ...
  };
  ...
```

### Authentication

Access tokens can be passed when creating a new service instance:

```typescript
const noteApi = new NoteApi({ accessToken: <access_token> });
```

## Create an object

```typescript
const noteParams: NoteParams = {
  text: "Hello from Stackprint!",
};
await noteApi.createNote({ noteParams });
```

## Get an object

```typescript
await noteApi.deleteNote({ id: "<id>" });
```

## List objects

```typescript
const response = await noteApi.listNotes();
const notes = response.data;
```

### Filter

```typescript
const response = await noteApi.listNotes({ author: "me" });
const notes = response.data;
```

### Sort

```typescript
const response = await noteApi.listNotes({ sort: "author:asc" });
const notes = response.data;
```

### Paginate

```typescript
const response = await noteApi.listNotes({ skip: 10, limit: 10 });
const notes = response.data;
```

## Update an object

```typescript
const noteParams: NoteParams = {
  text: "Hi from Stackprint!",
};
await noteApi.updateNote({ id: "<id>", noteParams });
```

## Delete an object

```typescript
await noteApi.deleteNote({ id: "<id>" });
```
