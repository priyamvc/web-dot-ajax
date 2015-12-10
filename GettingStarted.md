# Getting Started with Web.Ajax #



## Setting up to use Web.Ajax ##
  1. Add a reference to Web.Ajax.dll in your Asp.Net web project.
  1. Add the following handler to your web.config

```xml

```
<!--For Classic application pools-->
<system.web>
    <httpHandlers>
	<remove verb="*" path="resource.axd" />
	<add verb="GET,HEAD" path="resource.axd" type="Web.Ajax.Handlers.Resource" validate="true" />
    </httpHandlers>
</system.web>

<!--For Integrated application pools-->
<system.webServer>
    <handlers>
        <add name="ResourceHandler" path="resource.axd" verb="*" type="Web.Ajax.Handlers.Resource,Web.Ajax" resourceType="Unspecified" preCondition="integratedMode" />
    </handlers>
</system.webServer>
```
```

## Creating a Server Side Method (in the .aspx.cs file) ##
  1. In the code behind for your .aspx page, change your page to inherit from Web.Ajax.Page
  1. Add a static Method to your page class and annotate with the [Ajax](Ajax.md) attribute
```c#

```
    using Web.Ajax;

    public partial class Default : Web.Ajax.Page
    {
        [Ajax(Name="Ajax.SampleMethod")]    //The Name identifies the method on the client side
        public static SimpleResponse SampleMethod(int a, int b)
        {
              var res=new SimpleResponse();
              res.Data=a*b;
              return res;
        }
    }
```
```


## Calling the AJAX method from the client (in the .aspx file) ##
  1. Add a button with the onclick event="ClickMe();"
```html

```
<input type="button" onclick="ClickMe();" value="Call Ajax Method" />
```
```
  1. Add the following Javascript:
```javascript

```
<script type="text/javascript">
    function onAjaxComplete(r)
    {
         alert('Message for the server: ' + r.Data);
    }

    function ClickMe()
    {
          //An extra parameter is available on the client providing a javascript method
          //to call once the ajax request has completed.
          Ajax.SampleMethod(5, 10, onAjaxComplete);
    }
</script>
```
```
