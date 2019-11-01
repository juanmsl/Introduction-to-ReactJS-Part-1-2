# Todolist - Adding Styles

Now lets give styles to our app, as this guide is not about CSS or SCSS, I'll not explain the styles, only will give you the styles and classname you should use.

> If you want to give a different style or layout, fell free to do it.

Before begin, as I use SCSS to create the styles, I need to install a library, being so Webpack will compile the SCSS files to css.

{% hint style="info" %}
To know more about SCSS read this [article](https://sass-lang.com/guide).
{% endhint %}

To install this package install the library **`node-sass`**

```bash
yarn add node-sass
```

After install it, restart the development server.

## Class names

{% code-tabs %}
{% code-tabs-item title="src/modules/index.js" %}
```java
...
<main className="todolist-app">
...
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="src/components/groupList/index.js" %}
```javascript
...
  return (
      <form onSubmit={this.addGroup} className="group-list">
        <section>
          <h1 className="main-title">{title}</h1>
          <p className="description">{description}</p>
          <input type="text" value={inputValue} onChange={this.handleInput} className="input" />
          <section className="group-list__buttons">
            <button className="button active" onClick={this.addGroup} disabled={isDisableAddButton}>Add</button>
            <button className="button danger" onClick={deleteGroups} disabled={isDisableDeleteAllButton}>Delete all</button>
          </section>
        </section>
        <section className="group-list__items">
          {this.renderGroups()}
        </section>
        <button className="button danger" onClick={deleteSelectedGroup} disabled={isDisableDeleteButton}>Delete Group</button>
      </form>
    );
```
{% endcode-tabs-item %}
{% endcode-tabs %}

