[![GitHub release](https://img.shields.io/github/release/weexteam/weex-toolkit.svg)](https://github.com/weexteam/weex-toolkit/releases)  [![GitHub issues](https://img.shields.io/github/issues/weexteam/weex-toolkit.svg)](https://github.com/weexteam/weex-toolkit/issues)
![Node Version](https://img.shields.io/node/v/weex-toolkit.svg "Node Version")

Weex-Toolkit
============

Weex CLI toolkit

[Chinese Doc](./README-zh.md)

## Pre Install
some dependencies need recent version of npm to install

if your
```
$ node -v
```
output less then `6.0.0`, please upgrade your node at first
you can use `n` to install newer node or download in https://nodejs.org/
recommend the LTS version of node


## Install
```
$ npm install -g weex-toolkit
```

## Usage

```
Usage: weex <foo/bar/we_file_or_dir_path>  [options]
Usage: weex init [projectName]

选项：
  --port    http listening port number ,default is 8081           [默认值: 8081]
  --wsport  websocket listening port number ,default is 8082      [默认值: 8082]

Usage:weex <command>

where <command> is one of:

       init                                   create a vue project
       debug                                  start weex debugger
       compile                                compile we/vue file
       create                                 create a weexpack project 
       platform <add|remove> <ios|android>    add/remove ios/android platform
       plugin <add|remove> <pluginName>       add/remove weexplugin 
       run <ios|android>                      build your ios/android app and run

weex <command> --help      help on <command>                                               
```

## Examples

#### create a new vue project

```
$ weex init your_project_name
```
Your new project directory list below:

```
 |—— .gitignore
    |—— README.md
    |—— .eslintrc
    |—— .babelrc
    |-- app.js
    |—— assets
    |—— /src
    |     |—— foo.vue
    |—— /build
    |—— weex.html
    |—— index.html
```
Switch to the project directory and run:

```
npm install
```
Some npm commands you can use:

```bash
# build both two js bundles for Weex and Web
npm run build

# start a Web server at 8080 port
npm run serve

# start weex-devtool for debugging with native
npm run debug
```


#### preview a `vue file` using Weex HTML5 renderer 
```
$ weex your_best_weex.vue
```

#### preview a `we file` using Weex HTML5 renderer 
```
$ weex your_best_weex.we
```

And you can use playgroud app to scan the qrcode one the page to preview it on your mobile device

#### compile a `.we .vue file` to JS Bundle
```
$weex compile your_best_weex.we  .
```
`your_best_weex.we` will be transform to JS Bundle file `your_best_weex.js` , saved in your current directory

#### compile many `.we .vue files` to JS Bundle
```
$weex compile path/to/\*.vue,\*.js .
```
all .vue .we files of directory `path/to` will be compiled into directory `.` 

## weex debug command
#### usage
```
weex debug [options] [we_file|bundles_dir]
            
  Options:

    --help               output usage information
    -V, --verbose        display logs of debugger server
    -v, --version        display version
    -p, --port [port]    set debugger server port
    -e, --entry [entry]  set the entry bundlejs path when you specific the bundle server root path
    -m, --mode [mode]    set build mode [transformer|loader]
```

#### start debugger
```
$weex debug
```
this command will start debug server and launch a chrome opening `DeviceList` page.
this page will display a qrcode ,you can use `Playground App` scan it for starting debug.

#### start debugger with a we file
```
$weex debug your_weex.we
```
this command will compile `your_weex.we` to `your_weex.js`  and start the debug server as upon command.
`your_weex.js` will deploy on the server and displayed in `DeviceList` page as  another qrcode contain the url of your_weex.js


#### start debugger with a directory of we files
```
$ weex debug your/we/path  -e index.we
``` 
this command will build every file in your/we/path and deploy them on the bundle server. your directory will mapping to  http://localhost:port/weex/ 
use -e to set the entry of these bundles. and the url of "index.we" will display on device list page as another qrcode 

## pack command
details for [weexpack](https://github.com/weexteam/weex-pack)


## Integrate weexpack commands


[Weexpack](https://github.com/weexteam/weex-pack) helps to setup weex application from scratch quickly. With simple commands, developers could create a Weex project, add different platform template, could install plugins from local, GitHub or Weex market, could pack up his application project and run on mobile. For those who would like to share his own plugins, he could publish them to the Weex market.

Now weex-toolkit can run the same commands of weexpack because of the new architecture. If your directory is generated by weexpack, you can build your iOS or android app.

### weex platform and run commands

Use `platform add|remove` to add or remove Weex app template and run it in your target devices.

``` bash
$ weex platform add iOS 
```

Then run platform, you will see an iPhone simulator

``` bash
$ weex run ios
```




### weex plugin commands

If you want to use some plugins on the [weex market] (https://market.weex-project.io/), weex-toolkit is the right choice.

```bash
$ weex plugin add plugin_name
```
You need to specify the plugin name from market like "weex-chart":

``` bash
$ weex plugin add weex-chart
```

Remove some plugins(eg:weex-chart):

``` bash
$ weex plugin remove weex-chart
```

Learn more about [weexpack](https://github.com/weexteam/weex-pack)




## FAQ

#### #Environment
Please make sure your node version is above 6.0 and npm version is above 5.0.
If you want to change your npm registry origin, do not use `cnpm`, we recommend you to use `nrm` or command like `npm config set registry https://registry.npm.taobao.org`.

#### #Current working directory is not a weexpack project
Since the 1.0.9 version, the `weex init` command has been removed. If you want to create the weex project, create it with the` weex create` command.

#### #Permisiion denied
First of all ,please do not install with "sudo" 
If `permisiion denied` error occurs,please try `sudo chmod 777 /usr/local/lib/node_modules`

If you see the following error

```
Error:permission denied.Please apply the write premission to the directory: "/Users/yourUserName"
```
We suggest you run `sudo chmod 777 ~` or `mkdir ~/.xtoolkit&chmod 777 .xtoolkit`

#### #Fsevents wanted error
windows users may have fsevents installation problems, like:
```
fsevents@1.1.2: wanted {"os":"darwin","arch":"any"} (current: {"os":"win32","arch":"ia32"})
```
You should remove your `node_module` of weex-toolkit, run command like this:

```
npm install --no-optional weex-toolkit -g
``` 

#### #Vue dismatch error

Try:

```
weex xbind repair toolkit-repair
weex repair
```

#### #Upgrade Error
If you encounter an error during the upgrade process, please check your version of npm, the npm version should above 5.0.

Then reload it with the following command:
```
rm -rf ~/.xtoolkit
npm un weex-toolkit -g
npm i weex-toolkit -g
```

#### Android SDK Environment

If you want to run android project, you can use the [emulator of Android Studio](https://developer.android.com/studio/run/emulator.html) or a [real device](https://developer.android.com/studio/run/device.html)

If you install Android SDk by Android studio, you should make sure the [Android 6.0 API](https://developer.android.com/about/versions/marshmallow/android-6.0.html) is installed.

#### spawn E2BIG

This problem may occur when you use the commands `weex create/init/run/platform`.
You need to update your weexpack to latest version.
```
$ weex update weexpack
```
If there have some error while update package, please remove `~/.xtoolkit` before update.
```
$ rm -rf ~/.xtoolkit
$ weex update weexpack
```


#### #Tips

If you are in use during the process, first check your package version is up to date, you can run `weex -v` and use `weex update weex-devtool@latest` to upgrade your package.



## Issue & Feedback

 [Github Issue List](https://github.com/weexteam/weex-toolkit/issues)
