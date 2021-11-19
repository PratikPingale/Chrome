<h1 align="center">Sweet_Pop!</h1>

<p align="center"><img src="./assets/preview.png"></p>

<h3 align="center">Floating Navigation</h3>
<p align="center"><img src="./assets/navbar.gif"></p>

<h3 align="center">Auto-hide Scrollbars</h3>
<p align="center"><img src="./assets/scrollbar.gif"></p>

<h3 align="center">Context Menu</h3>
<p align="center"><img src="./assets/context.png"></p>

<h3 align="center">Library</h3>
<p align="center"><img src="./assets/library.png"></p>

## Folder structure

 .<br>
├─  assets<br>
│ ├─  context.png<br>
│ ├─  library.png<br>
│ ├─  navbar.gif<br>
│ ├─  preview.png<br>
│ ╰─  scrollbar.gif<br>
├─  css<br>
│ ├─  findbar.css<br>
│ ├─  floatingToolbox.css<br>
│ ├─  library.css<br>
│ ├─  overflowMenu.css<br>
│ ├─  popups.css<br>
│ ├─  reddit.css<br>
│ ├─  responsiveNavbar.css<br>
│ ├─  tabbar.css<br>
│ ├─  tweaks.css<br>
│ ╰─  urlbar.css<br>
├─  icons<br>
│ ├─  back.svg<br>
│ ├─  close.svg<br>
│ ├─  close_hover.svg<br>
│ ├─  closew.svg<br>
│ ├─  fox-transparent.gif<br>
│ ├─  home.svg<br>
│ ├─  infoico.png<br>
│ ├─  max_hover.svg<br>
│ ├─  max_restore.svg<br>
│ ├─  min.svg<br>
│ ├─  min_hover.svg<br>
│ ├─  reload.svg<br>
│ ├─  restore_hover.svg<br>
│ ├─  search.svg<br>
│ ├─  sonic.gif<br>
│ ├─  tab-loading.png<br>
│ ╰─  welcome-back.svg<br>
├─  LICENSE<br>
├─  programs<br>
│ ├─  local-settings.js<br>
│ ├─  mozilla.cfg<br>
│ ╰─  user.js<br>
├─  README.md<br>
├─  script<br>
│ ├─  hideScrollbar.uc.js<br>
│ ╰─  navbarToolbarButtonSlider.uc.js<br>
├─  userChrome.css<br>
├─  userContent.css<br>
╰─  utils<br>
  ├─  boot.jsm<br>
  ╰─  chrome.manifest<br>

### [`userChrome.css`](./userChrome.css)
This helps to customize Firefox User Interface.

### [`userContent.css`](./userContent.css)
This helps to customize web content like a specific site.

### [`floatingToolbox.css`](./css/floatingToolbox.css)
Makes the toolbox float. Can be accessed via hovering over top of browser.<br>
All imports are present in `css` folder as well.

### [`hideScrollbar.uc.js`](./script/hideScrollbar.uc.js)
It's now possible to autohide scrollbars.

### [`navbarToolbarButtonSlider.uc.js`](https://github.com/aminomancer/uc.css.js#navbar-toolbar-button-slider)
As this is a one-liner theme, one must drop some buttons to add sufficient space for urlbar and tabbar. That's why I mentioned in [issue 2](https://github.com/PROxZIMA/Firefox-Theme/issues/2) to move the add-ons to overflow menu. But this messed up with their widths. Take a look [here](https://www.reddit.com/r/FirefoxCSS/comments/n9asta/addons_width_changes_to_a_fixed_value_when_placed/). I did some temporary fix(which was not that good). But [u/MotherStylus](https://www.reddit.com/user/MotherStylus) came up with an awesome `uc.js` script.<br>
So basically this adds a button slider to navbar toolbar. [This](https://raw.githubusercontent.com/PROxZIMA/Firefox-Theme/master/assets/navbar.gif) is how it looks. Read the file description to configure it properly.

### [`user.js`](./programs/user.js)
Contains required user preferences.

## **But how does it work?**
Custom startup-script (aka [`mozilla.cfg`](./programs/mozilla.cfg) here) is loaded using [`local-settings.js`](./programs/local-settings.js). This startup-script adds "loader" scripts from `utils` folder that loads arbitrary javascript files from the `script` folder into Firefox<br>
`mozilla.cfg` also helps in setting local webpage as your homepage. Details in [Installation](#Installation).

NOTE: Firefox team has removed XBL from Firefox starting with version 72, so userChrome.js would not work :/

## Installation
1) Open `about:support` in new tab and click `Open Directory` near `Profile Directory`.

2) Open this directory in terminal and clone the repository

Note: If you already have a `chrome` folder under `Profile Directory`, rename it to `chrome2` or anything else so that after trying this theme you can easily restore your theme.

```console
$ cd {Your profile directory}

$ git clone https://github.com/PROxZIMA/Firefox-Theme.git chrome

$ cd chrome
```

NOTE: If you are planning to set a local page as home page then in [`mozilla.cfg`](https://github.com/PROxZIMA/Firefox-Theme/blob/da7531c7089380c5c6e4faf2f9f365eb1fd3e49d/programs/mozilla.cfg#L14) at line 13 change `newTabURL_` to the local page location

3) Install `utils` folder from [fx-autoconfig](https://github.com/MrOtherGuy/fx-autoconfig) in your `chrome` folder (make sure it matches above Folder Structure). Perform following changes in the `utils/chrome.manifest` file.

```diff
content userchromejs ./
-content userscripts ../JS/
-content userchrome ../resources/
+content userscripts ../script/
+content userchrome ../
+resource content-accessible chrome://userchrome/content/layout/contentaccessible/ contentaccessible=yes
```

4) Move `user.js`, `mozilla.cfg` and `local-settings.js` to their destination.

<details><summary>Linux / OS X</summary>
<br>

On `about:support` > `Application Binary` > `{Installation folder}firefox-bin`<br>
My `Installation folder` is `/usr/lib/firefox/`

```console
$ cp ./programs/user.js ../

$ cp ./programs/mozilla.cfg /usr/lib/firefox/

$ cp ./programs/local-settings.js /usr/lib/firefox/defaults/pref/
```
</details>

<details><summary>Windows</summary>
<br>

On `about:support` > `Application Binary` > `{Installation folder}firefox.exe`<br>
Generally `Installation folder` is `C:\Program Files\Mozilla Firefox\`

```powershell
> copy .\programs\user.js ..\

> copy .\programs\mozilla.cfg "C:\Program Files\Mozilla Firefox\"

> copy .\programs\local-settings.js "C:\Program Files\Mozilla Firefox\defaults\pref\"
```
</details>

5) Download [`navbarToolbarButtonSlider.uc.js`](https://github.com/aminomancer/uc.css.js/blob/master/JS/navbarToolbarButtonSlider.uc.js) and place it in `script` folder along with `hideScrollbar.uc.js`.

6) In Firefox, right click hamburger button > `customize toolbar` disable `Title Bar`, `Drag Space`, set Density to `compact` and Themes to `dark` or `light`

7) Open `about:support` > `Clear startup cache...` > `Restart` ***twice***

8) **Voilà**

## Configuration
1) `programs/user.js` contains user preferences that are automatically loaded at startup. So no need to manually set them during installation

2) To disable any of the `script/*.uc.js` either disable it from `Toolbar Menu > Tools > userscripts > script` or rename `*.uc.js` to `*`. Restart ***twice***, every time you enable/disable the script.

    - `Floating scrollbars` -> `userChromeJS.floatingScrollbar.enabled`.
    - `Floating toolbox` -> `userChromeJS.floatingToolbox.enabled`.

3) You can also edit `hideScrollbar.uc.js` to customize the scrollbars according to your taste

4) For adding your own customizations make changes in `myChanges.css` file under `css` folder.

5) If something breaks on your system then please raise a issue

6) [@ArataKamikaze](https://github.com/ArataKamikaze) mentioned in [#5](https://github.com/PROxZIMA/Sweet-Pop/issues/5) that [Firefox Color](https://addons.mozilla.org/en-US/firefox/addon/firefox-color) breaks/overwrite existing theme so disable the extension if you face similar issue.

## Credits
- I started with this amazing material theme : [MaterialFox](https://github.com/muckSponge/MaterialFox) by [muckSponge](https://github.com/muckSponge)

- One of the best dark theme for Firefox : [ShadowFox](https://overdodactyl.github.io/ShadowFox) by [overdodactyl](https://github.com/overdodactyl)

- Floating Toolbox : [u/oldworlds](https://www.reddit.com/r/FirefoxCSS/comments/koa71w/minimalfox_a_compact_and_minimal_theme/)

- [Theme inspiration](https://www.reddit.com/r/FirefoxCSS/comments/ci7i69/another_oneline_theme/) by [u/SENDMEJUDES](https://www.reddit.com/user/SENDMEJUDES/)

- [u/It_Was_The_Other_Guy](https://www.reddit.com/user/It_Was_The_Other_Guy) helped me a lot on [r/FirefoxCSS](https://www.reddit.com/r/FirefoxCSS/)<br>
Also this theme uses his [`fx-autoconfig`](https://github.com/MrOtherGuy/fx-autoconfig) to load the javascripts files.

- [`navbarToolbarButtonSlider.uc.js`](https://github.com/aminomancer/uc.css.js#navbar-toolbar-button-slider) script by [u/MotherStylus](https://www.reddit.com/user/MotherStylus) adds button slider to navbar toolbar. More details [here](https://www.reddit.com/r/FirefoxCSS/comments/n9asta/addons_width_changes_to_a_fixed_value_when_placed/)

- [Setting local page as homepage](https://www.reddit.com/r/firefox/comments/ge86z4/newtab_page_to_local_file_firefox_76_redux/)

- Auto hide scrollbars : details [here](https://www.reddit.com/r/FirefoxCSS/comments/jptrf8/is_it_still_possible_to_autohide_and_show/) by [u/mimecry](https://www.reddit.com/user/mimecry/)

- [Prism](https://github.com/PROxZIMA/prism): A minimalist, beautiful startpage forked from [Prismatic Night](https://github.com/3r3bu5x9/Prismatic-Night)

___
<p align="center">Made with ❤️</p>
<h2 align="center">ARIGATOU</h2>
