# NBN23 Embeddable Widget

This repository describes how to embed the NBN23 Widget in your website.

# Documentation

## Load the widget script

You'll need to load this script in your website:

`https://widget.nbn23.com/widget-react.js.gz`

The way to do this varies depending on how you website works. This are a few possible scenarios:

* Load the script the standard way by adding `<script src="//widget.nbn23.com/widget-react.js.gz" type="text/javascript"></script>`
* If you use WordPress or other CMS, you'll need to enqueue the script to your pages (or to a specific page within your website). For example, in WordPress you would do this: `wp_enqueue_script( 'widget-script', '//widget.nbn23.com/widget-react.js.gz' );`

## Initialize the script

The widget script exports a module called `swish_widget_app`. You will need to initialize the widget, using the `init` method:

```js
swish_widget_app.init({
  mountOn: "my_widget",
  apiKey: "apikeyTest",
  appDownloadUrl: "https://www.nbn23.com/es/swish-promo/"
});
```

After initializing the widget, it will render in the DOM node specified in the `mountOn` property. If that property is missing, the widget will try to render in a node with an ID `root`.

You will also need an apiKey provided by NBN23, which will be used to identify your organization and when querying our servers.

## Available init options

| Property                      | Type               | Description                                                                                            |
| ----------------------------- | ------------------ | ------------------------------------------------------------------------------------------------------ |
| mountOn                       | string             | HTML node where the widget will render. Defaults to 'root'                                             |
| theme                         | string             | If we have added a custom theme for your organization, we'll provide this value to you                 |
| apiKey                        | string             | Mandatory api key to query our servers                                                                 |
| appDownloadUrl                | string             | If specified, rows in the calendar view will be clickable and will open this URL                       |
| hideCalendar                  | Boolean            | Allows hiding the Calendar view                                                                        |
| hideStandings                 | Boolean            | Allows hiding the Standings view                                                                       |
| backgroundColor               | string             | By default, the widget background is transparent. You can change it by setting a hex color code here   |


