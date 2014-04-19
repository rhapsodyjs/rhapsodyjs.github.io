If enabled, you must add a hidden field to your forms using the the variable from locals called `_csrf`, like this:

```html
	<form action="/enter" method="post">
		<label for="user">Username</label>
		<input type="text" name="user" id="user">
		<input type="hidden" name="_csrf" value="{% raw  %}{{_csrf}}{% endraw  %}">
		<input type="submit">
	</form>
```