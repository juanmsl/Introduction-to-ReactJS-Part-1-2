# Todolist - Handling States

Great now we have the architecture of our components, now lets gonna give them functionality, handling their states.

## TodolistApp component

The sate of the main component, have the **`list of groups`** and the **`selected group`**, and as we know, their children depends on his state, so the responsibility to update his state is the **`TodolistApp`** component, and his children when they call the event to add a group or a task or delete them, should use the functionality of his parent, so lets gonna define the methods to handle the groups and tasks.

### addGroup

{% code-tabs %}
{% code-tabs-item title="src/modules/index.js" %}
```javascript
...
  addGroup = (name) => {
    const group = {
      name: name,
      tasks: []
    };
    this.setState((prevState) => ({
      groups: [...prevState.groups, group],
      selectedGroupIndex: prevState.groups.length
    }));
  }
...
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### deleteSelectedGroup

{% code-tabs %}
{% code-tabs-item title="src/modules/index.js" %}
```javascript
...
  deleteSelectedGroup = () => {
    const {groups, selectedGroupIndex} = this.state;
    groups.splice(selectedGroupIndex, 1);
    this.setState({
      groups: groups,
      selectedGroupIndex: null
    });
  }
...
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### deleteGroups

{% code-tabs %}
{% code-tabs-item title="src/modules/index.js" %}
```javascript
...
  deleteGroups = () => {
    this.setState({
      groups: [],
      selectedGroupIndex: null
    });
  }
...
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### addTask

{% code-tabs %}
{% code-tabs-item title="src/modules/index.js" %}
```javascript
...
  addTask = (text) => {
    const task = {
      text: text,
      done: false
    };
    const { groups, selectedGroupIndex } = this.state;
    const group = groups[selectedGroupIndex];
    group.tasks = [...group.tasks, task];
    groups[selectedGroupIndex] = group;
    this.setState({
      groups: groups
    });
  };
...
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### deleteTasks

{% code-tabs %}
{% code-tabs-item title="src/modules/index.js" %}
```javascript
...
  deleteTasks = () => {
    const {groups, selectedGroupIndex} = this.state;
    const group = groups[selectedGroupIndex];
    group.tasks = [];
    groups[selectedGroupIndex].tasks = [];
    this.setState({
      groups: groups
    });
  }
...
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### selectGroup

{% code-tabs %}
{% code-tabs-item title="src/modules/index.js" %}
```javascript
...
  selectGroup = (index) => {
    this.setState({
      selectedGroupIndex: index
    });
  };
...
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### toggleDoneTask

{% code-tabs %}
{% code-tabs-item title="src/modules/index.js" %}
```javascript
...
  toggleDoneTask = (taskIndex) => {
    const { groups, selectedGroupIndex } = this.state;
    const group = groups[selectedGroupIndex];
    const task = group.tasks[taskIndex];
    task.done = !task.done;
    groups[selectedGroupIndex].tasks[taskIndex] = task;
    this.setState({
      groups: groups
    });
  };
...
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Render method

Now after define how the **`TodolistApp`** component will handle his state, its turn to allow his children to use that methods, so we can pass a function as a prop to another component, and the other component can invoke that function, so Its turn to pass that functions as props to the children **`GroupList`** and **`TaskList`**.

#### GroupList

As we know which of these functions should use the **`GroupList`** component?

That component _**create**_ groups and _**delete**_ them, further more, can _**select**_ a group to show his tasks, so we should pass him the functions that allow do that. Also, if we want to enable/disable buttons and add an style to the selected group, the component should know _**which group is selected**_.

{% code-tabs %}
{% code-tabs-item title="src/modules/index.js" %}
```javascript
...
  <GroupList
    title="Todo List"
    description="In this list you can add a project to start planning your tasks about it"
    groups={groups}
    addGroup={this.addGroup}
    deleteGroups={this.deleteGroups}
    deleteSelectedGroup={this.deleteSelectedGroup}
    selectGroup={this.selectGroup}
    selectedGroup={selectedGroup}
  />
...
```
{% endcode-tabs-item %}
{% endcode-tabs %}

#### TaskList

Now, following the same logic we need to send to the component the function that should use.

{% code-tabs %}
{% code-tabs-item title="src/modules/index.js" %}
```javascript
...
  <TaskList
    group={selectedGroup}
    addTask={this.addTask}
    deleteTasks={this.deleteTasks}
    toggleDoneTask={this.toggleDoneTask}
  />
...
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Final component file

{% code-tabs %}
{% code-tabs-item title="src/modules/index.js" %}
```javascript
import React from 'react';
import {
  GroupList,
  TaskList
} from "components";

export default class TodolistApp extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      groups: [],
      selectedGroupIndex: null
    };
  }

  addGroup = (name) => {
    const group = {
      name: name,
      tasks: []
    };
    this.setState((prevState) => ({
      groups: [...prevState.groups, group],
      selectedGroupIndex: prevState.groups.length
    }));
  }

  deleteSelectedGroup = () => {
    const {groups, selectedGroupIndex} = this.state;
    groups.splice(selectedGroupIndex, 1);
    this.setState({
      groups: groups,
      selectedGroupIndex: null
    });
  }

  deleteGroups = () => {
    this.setState({
      groups: [],
      selectedGroupIndex: null
    });
  }

  addTask = (text) => {
    const task = {
      text: text,
      done: false
    };
    const { groups, selectedGroupIndex } = this.state;
    const group = groups[selectedGroupIndex];
    group.tasks = [...group.tasks, task];
    groups[selectedGroupIndex] = group;
    this.setState({
      groups: groups
    });
  };

  deleteTasks = () => {
    const {groups, selectedGroupIndex} = this.state;
    const group = groups[selectedGroupIndex];
    group.tasks = [];
    groups[selectedGroupIndex].tasks = [];
    this.setState({
      groups: groups
    });
  }

  selectGroup = (index) => {
    this.setState({
      selectedGroupIndex: index
    });
  };

  toggleDoneTask = (taskIndex) => {
    const { groups, selectedGroupIndex } = this.state;
    const group = groups[selectedGroupIndex];
    const task = group.tasks[taskIndex];
    task.done = !task.done;
    groups[selectedGroupIndex].tasks[taskIndex] = task;
    this.setState({
      groups: groups
    });
  };

  render() {
    const { groups, selectedGroupIndex } = this.state;
    const selectedGroup = groups[selectedGroupIndex];

    return (
      <main>
        <GroupList
          title="Todo List"
          description="In this list you can add a project to start planning your tasks about it"
          selectedGroup={selectedGroup}
          groups={groups}
          addGroup={this.addGroup}
          deleteGroups={this.deleteGroups}
          deleteSelectedGroup={this.deleteSelectedGroup}
          selectGroup={this.selectGroup}
        />
        <TaskList
          group={selectedGroup}
          addTask={this.addTask}
          deleteTasks={this.deleteTasks}
          toggleDoneTask={this.toggleDoneTask}
        />
      </main>
    );
  }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## GroupList component

### Input value

### Enable/disable buttons

### Prop functions

### Item onClick

### Final component file

