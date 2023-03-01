## HTML Helper Methods

### **Creating a link with ActionLink()**
Example: @Html.ActionLink("See all items", "Index", "Items")
1. The first parameter "See all items" is the display text for the link. In other words, a user will see a link that says "See all items".
2. The second parameter "Index" is the target action in the controller.
3. The third parameter Items is optional, and it specifies the controller that we want to route to. Since we've included this third parameter, this ActionLink will take us to the Index() route method in the ItemsController. If we don't include the optional third parameter the ActionLink method will default to the controller that corresponds to the view that the ActionLink method executes from.

### **Creating a form with BeginForm(), LabelFor() and TextBoxFor()**

Example: 

```c#
@{
  Layout = "_Layout";
}

@model ToDoList.Models.Item

<h4>Add a new item</h4>
@using (Html.BeginForm())
{
  @Html.LabelFor(model => model.Description)
  @Html.TextBoxFor(model => model.Description)
  <input type="submit" value="Add new item" />
}
<p>@Html.ActionLink("Show all items", "Index")</p>
```

- `@model ToDoList.Models.Item`

  A model directive tells our view what type of data will be passed into the view from the controller route. We can only include one @model directive in each view, just like we can only pass in one model to each View() method in our controllers.

- `@using (Html.BeginForm())`

  The using statement does is add a closing HTML \</form> tag to the form. The form sends an HTTP POST request by default. This form will send a POST request to the Create() route in the ItemsController because it is located in Views/Items/Create.cshtml.

- `LabelFor()` 
  Generates a label for a form field. It is a "strictly typed" helper. It requires the argument `model => model.Description` which specifies that we want to use the property name "description" for the form label.

- `TextBoxFor()` 
  Generates a text box form field. It is a "strictly typed" helper. It requires the argument `model => model.Description` which specifies that we want to use the property name "description" for the form label.

- We could do this instead:
  
  ```c#
  @using (Html.BeginForm())
  {
  @Html.Label("Description")
  @Html.TextBox("Description")
  <input type="submit" value="Add new item" />
  }
  ```
  But these helpers don't provide error checking at compile time.