The theming system is pretty straight forward. With minimal effort one could have there own skin in uw-frame. We extremely highly encourage you to contribute back your theme to this project so you don't have to manage an independent fork of uw-frame. Anyway, here are the steps to configure your theme:

+ Configure your entry in the `THEME` constant located in [`frame-config.js`](https://github.com/UW-Madison-DoIT/uw-frame/blob/master/uw-frame-components/js/frame-config.js). It should look something like :

```javascript
{
  "name" : "uw-madison",
  "crest" : "img/uw-madison-52.png",
  "title" : "MyUW",
  "subtitle" : null,
  "ariaLabelTitle" : "My U W",
  "crestalt" : "UW Crest",
  "group" : "UW-Madison",
  "mascotImg" : "img/bucky.gif",
  "footerLinks":[
                  { "url" : "/web/static/myuw-help",
                    "target" : "_blank",
                    "title" : "Help"
                  }
                ],
  "materialTheme" : {
    "primary" : "red",
    "accent"  : "blue",
    "warn"    : "orange"
  }
}
```
+ JSON above explained
  + `name`: the system id of the theme. Make sure its unique.
  + `crest` : The relative URL to the crest image. We recommend the crest image (in this example `img/uw-madison-52.png`) to be `52px` in height.  The image height will be set to `52px`, so the width will scale to fit that. Width doesn't really matter, but try to keep it under 100px for small screens.
 + `title` : The title that will be show in the upper right
 + `subtitle` : an `optional` subtitle that is shown as subtext for the app. e.g.: beta
 + `ariaLabelTitle` : The aria label put in place of the theme title
 + `crestalt` : the alt text
 + `group` : Which group should this be enabled for automatically? Not sure, ask the MyUW dev team.
 + `mascotImg` : (Optional) See documentation about the mascot for announcements [here](#/md/announcements)
 + `footerLinks` : An array of links which appear in the footer. Typically the campus help desk and feedback portal.
 + `materialTheme` : [object or string] See section below labeled Material Theme.

+ Add in a <theme-name>.less file in the folder `/uw-frame-components/css/themes` that looks like this:

  ```less
  @import "../angular.less"; //order is important here
  @import "common-variables.less";
  @import "uw-madison-variables.less";
  ```

In this example that is `uw-madison.less`. Notice I got the `uw-madison` from the name. That is important.

+ As you probably noticed above, you also will want to add in a `<theme>-variables.less` file in the same directory. This will be full of color variable declarations. Here is an example of that:

  ```
  /* UW-Milwaukee colors */
  @color1: #000000;         
  @color2: lighten(@color1, 5%);
  @color3: darken(@color1, 5%);
  @color4: #E1DCCC;
  @link-color: @color3;

  @state-info-bg: #999999;   // Olive Grey
  @state-info-text: #000000; // Black

  @portlet-titlebar-background-color: #E7D9C1;
  @portlet-border-color: #E7D9C1;

  @user-portal-logout-btn-text-color: #FFF; //White

  @input-border-focus: @color1;
  ```

  `@color1` is your primary color, in uw-madison's case, this is Badger Red, but for UW-Milwaukee this is Black. Its used for the banner, primary color of buttons, etc... `@color2` is a slightly lighter. For simplicity you can just use the lighten function in less, or you can specific a specific color. This is used for various sub important things. `@color3`: This is always slightly darker than `@color1` and it is used for links.

+ The last step is setting a default theme in your `override.js`. For more information on that see the [configuration](#/md/configuration) section under `APP_FLAGS` there is a variable called `defaultTheme`.

### Material Theme
Each theme can have a material theme. If it doesn't, it will use the Google default color selection for `primary`, `accent`, and `warn` palettes. Palette information can be found on the [angular material site](https://material.angularjs.org/latest/Theming/01_introduction). The `materialTheme` object has 3 attributes: `primary`, `accent`, and `warn`. Each attribute can be a string or an object.

If it is a string it will assume it is a precreated palette color, and look at the [angular material site](https://material.angularjs.org/latest/Theming/01_introduction) for created palettes.

e.g.:

```
"materialTheme" : {
  "primary" : "red",
  "accent"  : "blue",
  "warn"    : "orange"
}
```

If it is an object it will assume that it is a custom palette definition. e.g.:

```
"materialTheme" : {
  "primary" : {
    '50': 'FED5D7',
    '100': 'FC8B8F',
    '200': 'FB545A',
    '300': 'F90E17',
    '400': 'E3060E',
    '500': 'C5050C',
    '600': 'A7040A',
    '700': '890308',
    '800': '6B0307',
    '900': '4E0205',
    'A100': 'FED5D7',
    'A200': 'FC8B8F',
    'A400': 'E3060E',
    'A700': '890308',
    'contrastDefaultColor': 'light',    // whether, by default, text (contrast)
                      // on this palette should be dark or light
    'contrastDarkColors': ['50', '100', //hues which contrast should be 'dark' by default
      '200', '300', '400', 'A100'],
    'contrastLightColors': undefined    // could also specify this if default was 'dark'
  },
  "accent" : {
    '50': 'B8E9FD',
    '100': '6DD3FC',
    '200': '36C2FA',
    '300': '05A4E4',
    '400': '058FC6',
    '500': '0479A8',
    '600': '03638A',
    '700': '034E6C',
    '800': '02384E',
    '900': '012330',
    'A100': 'B8E9FD',
    'A200': '0479A8',
    'A400': '058FC6',
    'A700': '034E6C',
    'contrastDefaultColor': 'light',    // whether, by default, text (contrast)
                      // on this palette should be dark or light
    'contrastDarkColors': ['50', '100',
      '200', '300', '400', 'A100'],
    'contrastLightColors': undefined
  },
  "warn" : {
    '50': 'FFFFFF',
    '100': 'F9E7D7',
    '200': 'F2C9A6',
    '300': 'EAA368',
    '400': 'E6934D',
    '500': 'E28332',
    '600': 'D7731E',
    '700': 'BC651B',
    '800': 'A15717',
    '900': '874813',
    'A100': 'FFFFFF',
    'A200': 'F9E7D7',
    'A400': 'E6934D',
    'A700': 'BC651B',
    'contrastDefaultColor': 'light',
    'contrastDarkColors': ['50', '100',
      '200', '300', '400', 'A100'],
    'contrastLightColors': undefined
  }
}
```

### Testing
If you want to override your default theme just for testing or something we created an access point in the settings page. For the default frame we have that at `/settings`. There should be a drop down that has every theme listed in the `THEME` constant. Switch over and give it a whirl.

### More about multi-tenant themes
If you set `APP_FLAGS.defaultTheme` equal to `group` then on page load it will pull the list of groups your in (so make sure you set that service up), then it will try to match a group name with a theme's group variable. Case sensitive. First one found it caches that theme in session storage. On the next page refresh it checks the cache first, to avoid another group search.