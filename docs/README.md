This document provides an overview of the RDvue’s top-level _template.json &_ the _manifest.json_ of each module.

template.json
-------------

The _template.json_ file keeps a record of each abstracted template module. This file directs how the CLI will navigate and parse each subsequent template module. The following is a breakdown of the sections that make up _template.json._

The template.json file includes the following properties

### _version_

a number representing the current version of the file

![](https://realdecoy.atlassian.net/wiki/images/icons/grey_arrow_down.png)Example - click to expand

```
{
  "version": 1
}
```

### _sourceDirectory_

Source directory for module files that will be copied into a project. Normally points to the base folder of a module.

![](https://realdecoy.atlassian.net/wiki/images/icons/grey_arrow_down.png)Example - click to expand

```
{
  "sourceDirectory": "./",
}
```

### _features_

The features section holds a list of objects with each representing a single feature. Each object holds two properties, name & private.

The _name_ property holds the name of a feature, this the name that you **must** use when running a command on any of these features.

The _private_ is a boolean which determines whether or not the files of a feature can be overwritten after been initially added to the project. Also, features whose private property is set to _true_ cannot be added in by a user.

![](https://realdecoy.atlassian.net/wiki/images/icons/grey_arrow_down.png)Example - click to expand

```
  "features": [
    {
      "name": "config",
      "private": true
    },
    {
      "name": "store",
      "private": true
    },
    {
      "name": "component",
      "private": false
    },
    {
      "name": "service",
      "private": false
    },
    {
      "name": "model",
      "private": false
    },
    {
      "name": "page",
      "private": false
    },
    {
      "name": "sm",
      "private": false
    }
  ]
```

### _plugins_

The plugins section holds a list of names of the plugins available in RDvue. After setting up your configuration files for a plugin, simply add the name (the name of the _module_ folder for the configuration files of your plugin) to this list to make it available to the CLI for usage.

![](https://realdecoy.atlassian.net/wiki/images/icons/grey_arrow_down.png)Example - click to expand

```
"plugins": [
    "auth",
    "localization",
    "storybook"
  ]
```

### _project_

The _project_ section is an object which defines what will be installed at project creation. Currently, there are two properties/keys on this object, _features_ & _plugin._

_The features_ property/key is an array holding the name of all features which will be automatically generated at project creation.

The _plugins_ property/key is an array holding the name of all plugins which will be automatically generated at project creation.

![](https://realdecoy.atlassian.net/wiki/images/icons/grey_arrow_down.png)Example

```
"project": {
    "features": [
      "config",
      "store"
    ],
    "plugins": [
      "storybook"
    ]
  }
```

#### _groups_

The _groups_ section is used to group plugins that offer similar functionalities.

For example, imagine if we had the following two UI libraries _Buefy_ & _Vuetify_, we could create a group called _ui-library_ which holds these two plugins.

Each group is represented as an object. Each object has the following properties:

*   _name -_ the name of the group

*   _isMultipleChoice_ \- boolean indicating if more than one option can be selected from this group

*   _plugins_ - a list of the names of the plugins that belong to the group

*   _question_ \- the question prompted to a user when they run the command to add a plugin from a group


Running _rdvue add-group **<group\_name>**_ would prompt a user with the question that belongs to the requested group along with the list of plugins in that group to choose from.

![](https://realdecoy.atlassian.net/wiki/images/icons/grey_arrow_down.png)Example - click to expand

```
 "groups": [
    {
      "name": "authentication",
      "isMultipleChoice": false,
      "plugins": [
        "auth"
      ],
      "question": "Which Authentication Library would you like to install?"
    },
    {
      "name": "locale",
      "isMultipleChoice": false,
      "plugins": [
        "localization"
      ],
      "question": "Which Localization Library would you like to install?"
    }
  ],
```

#### _presets_

_presets_ are available for a user to quickly scaffold in _plugins_ when creating a project. The _presets_ section of the _template.json_ contains a list of objects. each representing an individual preset. A preset object contains the following properties:

*   _name_ \- the name of the preset

*   _description_ \- description of the preset. Conventionally used to list out the plugins that comes with the preset

*   _plugins_\- a list of the _plugins_ which the preset will install


![](https://realdecoy.atlassian.net/wiki/images/icons/grey_arrow_down.png)Example - click to expand

```
 "presets": [
    {
      "name": "Sample Preset 1",
      "description": "Installs storybook, and localization",
      "plugins": [
        "storybook",
        "localization"
      ]
    }
  ]
```

#### _customPreset_

A user can decide to manually select _plugins_ from different _groups_ that they’d like at project creation instead of choosing a _preset_. The _cutomPreset_ object describes the _groups_ available to a user. It includes the following:

*   _name_ \- the name displayed to the user

*   _groups_ \- a list containing the names of the Feature Groups which the user will be able to choose from


![](https://realdecoy.atlassian.net/wiki/images/icons/grey_arrow_down.png)Example - click to expand

```
 "customPreset": {
    "groups": [
      "authentication",
      "locale"
    ],
    "name": "custom"
  }
```

Here is a sample of what a complete template.json file would look like

![](https://realdecoy.atlassian.net/wiki/images/icons/grey_arrow_down.png)Example - click to expand

```
{
  "version": 1,
  "sourceDirectory": "./",
  "features": [
    {
      "name": "config",
      "private": true
    },
    {
      "name": "store",
      "private": true
    },
    {
      "name": "component",
      "private": false
    },
    {
      "name": "service",
      "private": false
    },
    {
      "name": "model",
      "private": false
    },
    {
      "name": "page",
      "private": false
    },
    {
      "name": "sm",
      "private": false
    }
  ],
  "plugins": [
    "auth",
    "localization",
    "storybook"
  ],
  "project": {
    "features": [
      "config",
      "store"
    ],
    "plugins": [
      "storybook"
    ]
  },
  "groups": [
    {
      "name": "authentication",
      "isMultipleChoice": false,
      "plugins": [
        "auth"
      ],
      "question": "Which Authentication Library would you like to install?"
    },
    {
      "name": "locale",
      "isMultipleChoice": false,
      "plugins": [
        "localization"
      ],
      "question": "Which Localization Library would you like to install?"
    }
  ],
  "presets": [
    {
      "name": "Sample Preset 1",
      "description": "Installs storybook, and localization",
      "plugins": [
        "storybook",
        "localization"
      ]
    }
  ],
  "customPreset": {
    "groups": [
      "authentication",
      "locale"
    ],
    "name": "custom"
  }
}
```

* * *

Template Module
===============

Modules are self-contained building blocks of a full Vue project. Each module must contain a manifest.json file.

manifest.json
-------------

The **manifest.json** file holds contextual knowledge of the structure of the current template module it resides in.

A _module.json_ file is built with the following section. _Not all sections will be needed inside every module.json file created. A module.json_ is composed of the following sections:

### version

The current version of the file

![](https://realdecoy.atlassian.net/wiki/images/icons/grey_arrow_down.png)Example - click to expand

```
  "version": 1,
```

### name

Name of the module (e.g store)

![](https://realdecoy.atlassian.net/wiki/images/icons/grey_arrow_down.png)Example - click to expand

```
  "name": "auth"
```

### description

A description of the module. This is also displayed inside the CLI help menu for each Module.

![](https://realdecoy.atlassian.net/wiki/images/icons/grey_arrow_down.png)Example - click to expand

```
  "description": "Generate a basic components needed for basic authenticaton."
```

### sourceDirectory

Source directory for module files that get copied into a project. Normally points to the base folder of a module.

![](https://realdecoy.atlassian.net/wiki/images/icons/grey_arrow_down.png)Example - click to expand

```
  "sourceDirectory": "./"
```

###
installDirectory

the location that the module should be generated in the **Vue** project.

![](https://realdecoy.atlassian.net/wiki/images/icons/grey_arrow_down.png)Example - click to expand

```
  "installDirectory": "./"
```

### files

a list of files that exist in the module that needs to be copied to the install directory. The files in this list can either be either of the following:

*   a _string_ (if the file should be copied as-is)


![](https://realdecoy.atlassian.net/wiki/images/icons/grey_arrow_down.png)Example - click to expand

```
"files": [
    {
      "source": "store/auth.ts",
      "target": "store/auth.ts"
    },
    {
      "source": "services/auth.ts",
      "target": "services/auth.ts"
    },
    {
      "source": "model/user.ts",
      "target": "model/user.ts"
    },
    {
      "source": "pages/register/index.ts",
      "target": "pages/auth/register/index.ts"
    },
    {
      "source": "pages/register/register.ts",
      "target": "pages/auth/register/register.ts"
    },
    {
      "source": "pages/register/register.scss",
      "target": "pages/auth/register/register.scss"
    },
    {
      "source": "pages/register/register.vue",
      "target": "pages/auth/register/register.vue"
    },
    {
      "source": "pages/login/index.ts",
      "target": "pages/auth/login/index.ts"
    },
    {
      "source": "pages/login/login.ts",
      "target": "pages/auth/login/login.ts"
    },
    {
      "source": "pages/login/login.scss",
      "target": "pages/auth/login/login.scss"
    },
    {
      "source": "pages/login/login.vue",
      "target": "pages/auth/login/login.vue"
    },
    {
      "source": "pages/forget-password/index.ts",
      "target": "pages/auth/forget-password/index.ts"
    },
    {
      "source": "pages/forget-password/forget-password.ts",
      "target": "pages/auth/forget-password/forget-password.ts"
    },
    {
      "source": "pages/forget-password/forget-password.scss",
      "target": "pages/auth/forget-password/forget-password.scss"
    },
    {
      "source": "pages/forget-password/forget-password.vue",
      "target": "pages/auth/forget-password/forget-password.vue"
    }
  ]
```

*   _object_ with required properties:
            - _source_ and _target_ (for change of name if necessary)
            - and an optional _content list_ of objects for finding and replacing content within the file -


![](https://realdecoy.atlassian.net/wiki/images/icons/grey_arrow_down.png)Example - click to expand

```
"files": [
    {
      "source": "index.ts",
      "target": "index.ts",
      "content": [
        {
          "matchRegex": "__COMPONENT__KEBAB__",
          "replace": "${componentNameKebab}"
        }
      ]
    },
    {
      "source": "component.scss",
      "target": "${componentNameKebab}.scss",
      "content": [
        {
          "matchRegex": "__COMPONENT__",
          "replace": "${componentNameKebab}"
        }
      ]
    },
    {
      "source": "component.ts",
      "target": "${componentNameKebab}.ts",
      "content": [
        {
          "matchRegex": "__COMPONENT__KEBAB__",
          "replace": "${componentNameKebab}"
        },
        {
          "matchRegex": "__COMPONENT__",
          "replace": "${componentName}"
        }
      ]
    },
    {
      "source": "component.spec.js",
      "target": "${componentNameKebab}.spec.js",
      "content": [
        {
          "matchRegex": "__COMPONENT__KEBAB__",
          "replace": "${componentNameKebab}"
        },
        {
          "matchRegex": "__COMPONENT__",
          "replace": "${componentName}"
        }
      ]
    },
    {
      "source": "component.vue",
      "target": "${componentNameKebab}.vue",
      "content": [
        {
          "matchRegex": "__COMPONENT__",
          "replace": "${componentNameKebab}"
        }
      ]
    }
  ]
```

_Note: files section can be a combination of both types mentioned above._

### packages

This section is an object that holds the npm packages to be installed with the module. This object contains two properties _dependencies and devDependencies._ Each holds a list of the name of the dependencies to be installed.

The _dependencies_ section holds dependencies required for the module to work (dev and production) while the _devDependencies_ section holds the dependencies that are only needed during development.

![](https://realdecoy.atlassian.net/wiki/images/icons/grey_arrow_down.png)Example - click to expand

```
 "packages": {
    "dependencies": ["vue-i18n"],
    "devDependencies": ["vue-cli-plugin-i18n"]
  }
```

There’s currently no support for specifying package versions.

### **routes**

_need assistance from_ [Tyrone Taylor](https://realdecoy.atlassian.net/wiki/people/5e0f5b85f65a6b0e9bf12539?ref=confluence) to discuss this section

### **vueOptions**

_need assistance from_ [Tyrone Taylor](https://realdecoy.atlassian.net/wiki/people/5e0f5b85f65a6b0e9bf12539?ref=confluence) to discuss this section

### **modules**

_need assistance from_ [Tyrone Taylor](https://realdecoy.atlassian.net/wiki/people/5e0f5b85f65a6b0e9bf12539?ref=confluence) to discuss this section