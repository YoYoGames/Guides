# Extension Contributions

All code repositories for GameMaker extensions can be found under https://github.com/YoYoGames/. Extension repository names start with the prefix `GMEXT-`.

You can contribute to extensions by reporting bugs and contributing code and/or documentation.

## Contributing Code

To contribute code or documentation to an extension: 

1. Fork the project.
2. If you're contributing code to the extension: make your changes to the code.
3. Add documentation for the changes that you made to the code in the `docs` folder or add documentation without making any changes to the code.
4. Create a pull request into the `main` branch with your changes for the extensions team to review.
5. If any changes to your pull request are required you will be asked to make them before the changes to the extension can be merged in.

After your pull request is merged into `main`, the extensions team will update the extension documentation on the wiki.

## Contributing Documentation

You can make changes to extension documentation if you find anything that should be changed or if any information is missing. When you add functionality to an extension, for example GML wrapper functions for API functions that aren't in the extension yet, you should also provide documentation for them.

### The "docs" Folder

All documentation for an extension is stored in a `docs` subfolder in the extension's code repository. The documentation on the wiki is generated from this.

The `docs` folder can contain the following: 

* One or more `*.js` files that store the documentation in a format similar to JSDoc.
* Optionally, one or more `*.md` pages. These pages can contain information on things like setting up the extension, getting started, etc.
* An `assets` subfolder that stores assets, such as images.

### Entities

The format of the documentation in the `*.js` files follows a syntax similar to [JSDoc](https://jsdoc.app) and GameMaker's [JSDoc Script Comments](https://manual.gamemaker.io/monthly/en/The_Asset_Editors/Code_Editor_Properties/JSDoc_Script_Comments.htm).

You can declare the following entities inside a comment block: 

* [`module`](#module)
  * `section` (`section_func`, `section_struct` and `section_const`)
* [`func`](#function-func) (or `function`)
  * `event`
* [`struct`](#struct)
* [`const`](#constant-const) (or `constant`)

These entities are mostly independent of each other with the exception of `event` (which must always be nested inside a `function` and allows multiple) and `section` and its variations (which must always be nested inside a `module` and allows multiple).

> **Note** There is also the [`page`](#page) entity, which you cannot declare directly yourself; it is used to refer to Markdown files in the directory.

A section must start with the tag `@<entity_name>` and end with the tag `@<entity_name>_end`. Everything inside those tags belongs to the given entity. For example: 

```js
/**
 * @func my_function_that_triggers_event
 * @desc This is a function.
 * 
 * @event social
 * @desc This event will be triggered by the function.
 * @member {boolean} success Whether the call was successful.
 * @event_end
 * 
 * @func_end
 */
```

The entities that you define are functions, constants and structs. You should always refer to them in a `module` using an `ref` inside a `section` to include them in the final documentation. A function, constant or struct that isn't referenced by any module will not be included.

```js
/**
 * @module my_module
 * @title My Module
 * @desc This is my module.
 * 
 * @section Functions
 * @desc This section lists a single function. It can also contain just some text (multiline).
 * @ref func.my_function_that_triggers_event
 * @section_end
 * 
 * @module_end
 */
```

You can also create sections that only contain references to a single type of entity with `section_func`, `section_const` and `section_struct`. In this case, the type prefix can be omitted: 

```js
/**
 * @module my_module
 * 
 * @section_func Functions
 * @ref my_function_that_triggers_event
 * @section_end
 * 
 * @section_const Constants
 * @ref pi_plus_phi
 * @section_end
 * 
 * @section_struct Structs
 * @ref my_struct
 * @section_end
 * 
 * @module_end
 */
```

You can also refer to Markdown pages (`*.md`) in the `docs` folder through the `page` entity. The filename without the `.md` extension is the name: 

```js
/**
 * @module my_module
 * 
 * @section Guides
 * @ref page.setting_up
 * @ref page.getting_started
 * @section_end
 * 
 * @module_end
 */
```

### Inserting Entities

You can refer to entities that you've defined as well as built-in GameMaker functions, structs and constants anywhere in the text using the syntax `${<type>.<identifier>}`. Inside a comment section: 

```js
/**
 * @func my_function
 * @desc This function does things.
 * 
 * You can make the function do more things by reading more data using ${function.buffer_read}.
 * 
 * You can use the constant ${constant.pi_plus_phi} for optimal results.
 * 
 * @func_end
 */
```

> This function does something.
> 
> You can make the function do more by reading more data using [buffer_read](https://manual.gamemaker.io/monthly/en/GameMaker_Language/GML_Reference/Buffers/buffer_read.htm).
>
> You can use the constant [pi_plus_phi](constants#pi_plus_phi) for optimal results.

As well as on an `*.md` page: 

```
The function ${function.fmod_system_init}, the constant ${constant.FMOD_RESULT} and the struct ${struct.FmodVector} are all part of the FMOD extension. General FMOD functions can be found in the ${module.system} module. Before that, you should read the ${page.getting_started} page to set up the extension properly.
```

> The function [fmod_system_init](system#fmod_system_init), the constant [FMOD_RESULT](constants#fmod_result) and the struct [FmodVector](structs#fmodvector) are all part of the FMOD extension. General FMOD functions can be found in the [System](system) module. Before that, you should read the [Getting Started](getting_started) page to set up the extension properly.

### Tag Reference

> **WARNING** All identifiers must be in lowercase (e.g. `my_function`).

#### module

A `module` groups functions, structs and constants under one or more sections. It can also have text-only sections.

Any function, struct or constant that is referenced by a module is included in the generated documentation.

```js
/**
 * @module <identifier>
 * @title Module
 * 
 * @section text_only_section
 * @desc This section contains only text. You can use it to add a header with some text to a module page.
 * @section_end
 * 
 * @section functions_1
 * @desc This is the first group of functions.
 * @ref func.first_function
 * @ref func.second_function
 * @section_end
 * 
 * @section_func functions_2
 * @desc This is the second group of functions.
 * @ref func.third_function
 * @ref func.fourth_function
 * @section_end
 * 
 * @module_end
 */
```

#### function (func)

A `function` documents a function of the extension.

```js
/**
 * @func <identifier>
 * @desc <multiline text>
 * @param {type} var description
 * @param {type} [optional_var="default"] optional parameter description
 * @return {type}
 * 
 * @example
 * 
 * @version
 * 
 * @func_end <multiline text> (end description)
 */
```

> **NOTE** If the function triggers multiple events or triggers the same event with different output (e.g. different keys in the `async_load` variable) you should add an `event` for every one of these.

#### event

An `event` documents an async event triggered by a function. It can only go inside a function entity.
It can have a description and has members, which are the members of the `async_load` DS map.

```js
/**
 * @func <identifier>
 * 
 * @event <type>
 * @desc <multiline text> (the description for the event data)
 * @member {type} <identifier> <multiline text> (adds a member to the async_load DS map)
 * @member 
 * 
 * @event_end <multiline text> (end description)
 * 
 * @func_end
 */
```

#### struct

A `struct` documents a [struct](https://manual.gamemaker.io/monthly/en/GameMaker_Language/GML_Overview/Structs.htm). Member variables of the struct are defined with `@member`.

```js
/**
 * @struct <identifier>
 * @desc <multiline text> (the description for this struct)
 * @member {type} <identifier> <multiline text>
 * @struct_end <multiline text> (end description)
 */
```

#### constant (const)

A `constant` documents either an enum, a group of similarly named constants or a single constant value, i.e. it documents anything that you'd call a [Constant](https://manual.gamemaker.io/monthly/en/GameMaker_Language/GML_Overview/Variables/Constants.htm) in GameMaker.

For example: 

```gml
// Enum
enum FMOD_DEBUG_MODE
{
    TTY,
    FILE,
    CALLBACK
};

// Similarly named constants
#macro FMOD_PRESET_OFF        {/* ... */}
#macro FMOD_PRESET_GENERIC    {/* ... */}
#macro FMOD_PRESET_PADDEDCELL {/* ... */}
// Etc.

// Single constant
#macro FMOD_VERSION    0x00020215
```

```js
/**
 * @const <identifier>
 * @desc <multiline text> (the description for this constant group)
 * @member <identifier> <multiline text> (adds a specific macro or constant value)
 * @const_end <multiline text> (end description)
 */
```

#### section

A `section` lists functions, constants and structs of a module or can contain just text in its description.

```js
/**
 * @module module
 * 
 * @section <identifier>
 * @desc <multiline text> (the description for this section)
 * @ref <pattern> (will match a single or a group of functions, constants, structs - allows multiple, NOTE that you need to identify the type you are trying to match using the prefix function. or constant. or struct. before the actual matching expression.)
 * @section_end <multiline text> (end description)
 * 
 * @module_end
 */
```

#### page

A `page` refers to an `*.md` page in the `docs` folder.

> **TIP** Use `@title <title>` at the top of an `.md` page to provide its title.