
Bootstrap MVC.Net
-----------------

This is a small set of HTML helper extension methods to help with using Twitter Bootstrap with ASP.NET MVC.

One key difference between the way the MVC helper methods work and the way Bootstrap works is in the area of label and button elements. 
In particular, MVC treats them separately, while Bootstrap requires the button to be nested within the label.

The label extension methods in this library borrow heavily from the way forms are handled in MVC.
They use the using statement and the IDisposable interface to enable the label wrapping structure, while preserving the ability to use existing extension methods for the buttons themselves.

```C#
@using (Html.BeginLabelFor(m => m.CheckMe, new { @class = "checkbox" })) {
    @Html.CheckBoxFor(m => m.CheckMe)
}
```

Note the inclusion of the htmlAttributes parameter. This is required for Bootstrap's label selector.

```HTML
<label class="checkbox" for="CheckMe">
    <input type="checkbox" name="CheckMe" value="true" /> Hey, Check Me!
</label>
```

As with normal LabelFor helpers, if you provide a DisplayAttribute for your model property, the Name text will be emitted.
Note, however, that it is emitted _after_ the nested helper is rendered, just prior to the closing </label> tag.

```C#
    [Display(Name = "Hey, Check Me!")]
    public bool CheckMe { get; set; }
```

The BeginLabel[For] helpers mirror those in ASP.NET MVC, as such, they fall under the same Apache 2.0 license.
I have taken the liberty to include them in the System.Web.Mvc.Html in order to simplify their use.
If you would like to put them into a different namespace, remember to reference the namespace with a @using directive to your view.
As an alternative, you can add a new namespace reference to the Web.config file in your Views directory.
