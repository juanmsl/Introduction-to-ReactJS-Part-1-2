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

Handle the state for this component is easier than the main component, as it only have the **`input value`** on his state. Now as we pass to the input as value the state, we need to update the state when the input changes, so we'll use the event **`onChange`** over the input.

{% hint style="info" %}
We use controlled components to handle form inputs, if you want read the next articles to understand more about [controlled components](https://en.reactjs.org/docs/forms.html#controlled-components) and [uncontrolled components](https://en.reactjs.org/docs/uncontrolled-components.html).
{% endhint %}

As the events in components needs as callback a function that receive the event, we need to create that function before specify the **`onChange`** event over the input.

{% code-tabs %}
{% code-tabs-item title="src/components/groupList/index.js" %}
```javascript
...
  handleInput = (e) => {
    e.preventDefault();
    const {value} = e.target;
    this.setState({
      inputValue: value
    });
  };
...
  <input type="text" value={inputValue} onChange={this.handleInput} />
...
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Enable/disable buttons

Now to enable and disable buttons depends on the state of the main component, so we need to define when each button is disable.

If the input value is empty, the add button should be disabled.

If there are not groups, the delete all groups button should be disabled.

If there are not any group selected, the button to delete the current group should be disabled.

{% code-tabs %}
{% code-tabs-item title="src/components/groupList/index.js" %}
```javascript
...
  const isDisableAddButton = inputValue === "";
  const isDisableDeleteAllButton = groups.length === 0;
  const isDisableDeleteButton = selectedGroup === undefined;
...
  <button disabled={isDisableAddButton}>Add</button>
  <button disabled={isDisableDeleteAllButton}>Delete all</button>
  <button disabled={isDisableDeleteButton}>Delete Group</button>
...
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Prop functions

Now its time to use those functions that we receive as props, those functions will be called when the user clicks on the buttons, so, we should use the **`onClick`** event in the buttons. As the events need a function that receive the event as parameter, the function that receiver params, as **`addGroup(name)`** for example, we need to use it on a local function that receive the event only.

{% code-tabs %}
{% code-tabs-item title="src/components/groupList/index.js" %}
```javascript
...
  addGroup = (e) => {
    e.preventDefault();
    const {inputValue} = this.state;

    if(inputValue === "") return;

    this.props.addGroup(inputValue);
    this.setState({inputValue: ""});
  };
...
  const {deleteGroups, deleteSelectedGroup} = this.props;
...
  <button onClick={this.addGroup} disabled={isDisableAddButton}>Add</button>
  <button onClick={deleteGroups} disabled={isDisableDeleteAllButton}>Delete all</button>
  <button onClick={deleteSelectedGroup} disabled={isDisableDeleteButton}>Delete Group</button>
...
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Item onClick

### Final component file

