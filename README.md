# NBN23 Embeddable Widget

This repository describes how to embed the NBN23 Widget in your website.

## Immplementation

### 1. Load the widget script

You'll need to load this script in your website:

`https://widget.nbn23.com/widget-react.js.gz`

The way to do this varies depending on how you website works. This are a few possible scenarios:

- Load the script the standard way by adding `<script src="//widget.nbn23.com/widget-react.js.gz" type="text/javascript"></script>` at the `<Head />` of your website.
- If you use WordPress or other CMS, you'll need to enqueue the script to your pages (or to a specific page within your website). For example, in WordPress you would do this: `wp_enqueue_script( 'widget-script', '//widget.nbn23.com/widget-react.js.gz' );` inside the `functions.php` file of your theme.

### 2. Initialize the script

The widget script exports a module called `swish_widget_app`. You will need to initialize the widget at the end of the `<Body />`, using the `init` method:

```html
<script>
  swish_widget_app.init({
    mountOn: "my_widget",
    apiKey: "apikeyTest",
    appDownloadUrl: "https://www.nbn23.com/es/swish-promo/",
  });
</script>
```

The configuration value that you should pay attention is `mountOn`, this value should be the `id` of the HTML node (div, span, p, etc.) you want the widget to be displayed.

After initializing the widget, it will render in the DOM node specified in the `mountOn` property. If that property is missing, the widget will try to render in a node with an ID `root`.

You will also need an `apiKey` provided by NBN23, which will be used to identify your organization, when querying our servers.

### Available init options

| Property        | Type    | Description                                                                                          |
| --------------- | ------- | ---------------------------------------------------------------------------------------------------- |
| mountOn         | string  | The "id" of the HTML node where the widget will be rendered. Defaults to 'root'                      |
| theme           | string  | If we have added a custom theme for your organization, we'll provide this value to you               |
| apiKey          | string  | Mandatory api key to query our servers                                                               |
| appDownloadUrl  | string  | If specified, rows in the calendar view will be clickable and will open this URL                     |
| hideCalendar    | Boolean | Hides the Calendar view                                                                              |
| hideStandings   | Boolean | Hides the Standings view                                                                             |
| backgroundColor | string  | By default, the widget background is transparent. You can change it by setting a hex color code here |

## Example

An example of how it would look on a simple HTML Page

```html
<html>
  <head>
    <title>Widget Test</title>
    <script
      src="//widget.nbn23.com/widget-react.js.gz"
      type="text/javascript"
    ></script>
  </head>

  <body>
    <div id="my_widget"></div>
    <script>
      swish_widget_app.init({
        mountOn: "my_widget",
        apiKey: "myApiKey",
        theme: "black",
        appDownloadUrl: "https://www.nbn23.com/es/swish-promo/",
      });
    </script>
  </body>
</html>
```

## Common problems

"This widget mount node hasn't been found. Check that the `mountOn` parameter in the configuration is correct or that you have a `"root"` node"

> The problem occurs when the widget is initialized and cannot find the HTML node specified in the `"mountOn"` field. This parameter is used to tell the widget where it should be mounted, and it should be the "id" of that HTML node (div, span, p, etc.). The cause of the problem can be two reasons:
>
> - The id specified in the `"mountOn"` field is incorrect or does not exist.
> - The widget is being initialized in the `<Head />` of the HTML; this causes the widget to try to mount on a node that has not yet been rendered
