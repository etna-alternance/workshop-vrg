---
title: [QuakeC basics - Quake Wiki, QuakeC - Good Practices]
source: [https://quakewiki.org/wiki/QuakeC_basics, https://quakewiki.org/wiki/QuakeC_Good_Practices]
---

## QuakeC Language Basics

- [QuakeC Simple Types](https://quakewiki.org/wiki/QuakeC_Simple_Types "QuakeC Simple Types")
- [QuakeC Field Types](https://quakewiki.org/wiki/QuakeC_Field_Types "QuakeC Field Types")
- [QuakeC Comments](https://quakewiki.org/wiki/QuakeC_Comments "QuakeC Comments")
- [QuakeC Names](https://quakewiki.org/wiki/QuakeC_Names "QuakeC Names")
- [QuakeC Structures and Objects](https://quakewiki.org/wiki/QuakeC_Structures_and_Objects "QuakeC Structures and Objects")
- [QuakeC Operators](https://quakewiki.org/wiki/QuakeC_Operators "QuakeC Operators")
- [QuakeC Definition of Functions](https://quakewiki.org/wiki/QuakeC_Definition_of_Functions "QuakeC Definition of Functions")
- [QuakeC Loops and Conditions](https://quakewiki.org/wiki/QuakeC_Loops_and_Conditions "QuakeC Loops and Conditions")
- [QuakeC Source Code of Vanilla Quake](https://quakewiki.org/wiki/Quake_QuakeC_source "Quake QuakeC source")

## FTEQCC Compiler Documentation

https://www.triptohell.info/moodles/fteqcc/README.html

## Alternate Resources

- Inside3D's QC Specs documentation: [\[1\]](http://www.insideqc.com/qcspecs/qc-menu.htm)

## Good Practices

This page is meant to act as a general guide for best practices to QuakeC and is not fully comprehensive. This guide will assume the latest version of FTEQCC is being used as it offers the fullest set of functionality while remaining vanilla compatible.

## Structure

Below is a guideline of ways to best structure your code base.

### Keep Functions General

One problem QuakeC has is often relying on changing the **self** pointer to execute certain functions, like so:

```
entity curSelf = self;
self = e;
DoFunction();
self = curSelf;
```

While sometimes this is inevitable, a simpler solution is to allow passing of the entity instead of relying on the **self** pointer:

```
DoFunction(e);
```

In general you want to avoid changing who **self** is pointing towards to reduce possible bugs. For cases where it is needed (such as setting monster states), using wrapper functions can help:

```
void CallAsSelf(entity e, void() func)
{
    entity curSelf = self;
    self = e;
    func();
    self = curSelf;
}

CallAsSelf(e, DoFunction);
```

This allows all the logic to be centralized across the entire code base, limiting potential bugs.

### Keep Files Clean

Don't scatter general logic across multiple unrelated files. Try and keep all functionality in a file as relevant to that specific type of entity as possible. For instance, attack check functions for specific monsters shouldn't be located in general monster logic files, nor should something like a general BSP entity mover be located within a random platform file. Keeping things grouped accordingly makes it much easier to maintain your code base and change it if tweaks are needed.

Avoid overlapping entity types in the same file as well if they have entirely separate functionality. Even if the entity is rather small, adding an extra file is always free. If a general logic file becomes too big, try and see if there's a way to sub-categorize the logic. For instance, instead of throwing the entire monster AI into one file, consider splitting it up based on searching logic vs chasing logic vs attacking logic. Folders can help greatly with keeping this managed.

### Avoid Globals

For overarching gameplay logic that the server manages, globals can work well. In this case these are functions where only one instance of logic can ever be active at a time e.g. the intermission timer.

For entity-specific logic, however, globals can cause a whole mess of bugs. Since multiple entities could be using those variables within the same frame, they'll all begin to use the wrong values (or more specifically, they'll use the values of the last entity to use them). There are two important questions to ask in regards to globals:

1. Does this need to be a global at all? Some logic could be broken down into simple local variables as the entity has no need for those globals after it finishes a single function. If values need to be passed around, use parameters instead.
2. Should this be an entity field instead? Sometimes something is best stored on a per-entity basis and has no meaning being stored globally.

### Avoid Egregious Reuse of Entity Fields

There are a lot of entity fields available, and not all of them may be in use on your entity. It can be tempting to swoop in and use one, but only do so if the name of the field makes sense. Storing important logic in seemingly nonsensical values can make it extra difficult to debug if something goes wrong. Consider how that field is used normally and what expectations someone will have trying to use it. You probably shouldn't store a movement cool down on a BSP entity in its **attack\_finished** field, after all.

If no existing field makes sense for your entity's case, just create a new one with an appropriate name. This will make it easier to maintain and for mappers to work with.

### Avoid Magic Numbers

A magic number is any value that can be hard to decipher its exact purpose at a glance. This might be something like the current state for a state-tracking variable. Instead, use constants to give numbers like this a named purpose that's instantly understood. For number ranges that are grouped in functionality, consider using an enum instead so it's obvious they're bundled.

### Avoid Functions Doing Too Many Things

If you find your function performing a bunch of different functionality, consider splitting it up into parts. Try and find any possible redundancies that could be split off into their own functions for reuse elsewhere. If performance is a concern, make sure to denote sections of your code properly with comments to make it easier to read.

For large switch cases/if else chains, consider seeing if some kind of entity field could be used instead. For instance, instead of hardcoding a wake up sound based on the entity's class, use a `wakeUpSound` field and have the function play that.

### Null Handling

Prefer using the `__NULL__` keyword over something like `SUB_Null()`. This will improve code flow as you'll no longer have to check if a valid function isn't also the empty one.

### Keep Function Arguments Clean

If a common default value is expected for a function argument, assign it explicitly:

```
float A_IsVisible(entity e, float ignoreWater = FALSE) {}
```

Even if the compiler will assign `FALSE` by default if the argument is left out, do not let it. Always be explicit.

If a function is beginning to have too many arguments, consider bundling them in a struct and passing that:

```
typedef struct
{
     float arg1, arg2, arg3;
     entity e;
     vector pos;
} MyFuncParams;
```

Use Pascal casing for structs meant to act as wrappers and use all lower case for structs meant to act as data types. Data types should have the `_t` suffix at the end to denote them.

### Keep Branching Simple

Try to avoid as much redundant code as possible when using loops and if/else statements. If you find yourself repeating the same code in a bunch of different else cases, consider restructuring it so it all converges onto one branch.

When using loops, always choose the right one for the job. If you're iterating over entities or using a counter, a for loop works best:

```
for (float i = 0; i < max; ++i)
```

This will guarantee your final statement is executed, even if you use `continue` allowing for cleaner code structure. If you're not sure if something will loop, use a while loop. If you need something to execute at least once, use a do-while loop.

Avoid unnecessary exit conditions that could easily be handled in the loop condition.

### Remove Unused Logic

If a variable is doing nothing, remove it. If a part of your function is no longer needed, don't just comment it out. Your code will be easier to read and maintain if useless logic is kept out.

### Avoid Comment Spam

Most things should be self explanatory with proper naming conventions. Comments are best left for explaining *why* something was made the way it was, not how something works specifically. For instance, you might leave a comment pointing out a piece of weird looking logic is used to avoid a bug and what that bug is.

## Naming Conventions

These are general guidelines for how to name things. Some of these are for improved integration with mapping tools like TrenchBroom while others are solid tips for making your code base easier to maintain.

### Entity Type Names

Generally entity types will start with what class they are as a prefix followed by their actual name. These are usually all lower case and use underscores to delimit separate words:

```
monster_ogre
trigger_secret
func_door
```

Monsters start with `monster_`, triggers start with `trigger_`, BSP entities like platforms and doors start with `func_` (short for function), pickups start with `item_`, weapons start with `weapon_`, and lights start with `light_`. For less general classes, use your own discretion as to what to call them, but make sure to keep it consistent. Other common classes used include `misc_` and `info_` (for entities only meant to act as information for another entity).

### Functions

Functions have no standard naming conventions within the base code, using all kinds of different conventions, but it's best to pick one and stick with it:

```
myFunction()
MyFunction()
my_function()
```

Only choose one of these to use. Consistency will make it easier for others to read and work on your code base should they desire. Do not use all capitals or all lower case without underscores. Avoid putting things like numbers in your function names.

There are three main types of function patterns used in QuakeC:

- Those meant to work on **self**.
- Those meant to act as states for a specific entity.
- Those meant to work on anything or nothing.

It can be best to give prefixes to these to help denote what type of function is meant to work on what at a glance. As an example:

- Use the `A_` prefix for functions meant to work on **self** (short for Action, similar to Doom's internal naming convention).
- Use the `S_` prefix for functions meant to act as entity states (short for State).
- Use no prefix for functions meant to work on anything or nothing.

Feel free to use whatever prefixes you desire, but it should be kept reasonable. This might also help catch potential oversights you had due to erroneous assumptions about what a function does.

Make sure the name of your function is descriptive. For instance, if your function returns a boolean value (`TRUE` or `FALSE`), the function should be asking a question e.g. `IsVisible()`. Functions that perform actions should include a verb describing what they do e.g. `FindNewEnemy()`. Avoid overly general names like `UpdateMonster()` as it's not obvious at a glance how this is actually updating it. Don't get too verbose, however, as the function can become annoying to work with.

For functions meant to be tied to callbacks, consider using some kind of naming convention. For instance, a function meant to be used as a `touch()` function might be called `MyEntityTouch()` or for `blocked()`, `my_entity_blocked()`. This will make it obvious what its usage is from a glance.

Avoid prefixes and suffixes if they serve no purpose.

### Variables

Using all capitals delimited by underscores is preferred for constants:

```
const float MY_CONST = 1;
```

Using `const` is not necessary but helps make the intention more explicit. For non-strongly typed enums, this is also the preferred convention. It's best to use some kind of prefix here to denote what the value is related to:

```
enum
{
    EN_VALUE1,
    EN_VALUE2
};
```

For strongly typed enums, it's better to use only Pascal casing:

```
enum class MyEnum : float
{
    Value1,
    Value2
};
```

Similar to functions, Quake's base code has no standard naming convention for variables:

```
myVar
my_var
```

Choose only one and stick with it. Avoid all capitals and all lower case without underscores. Pascal casing should only be used for public fields that are meant to act as properties:

```
.string DamageType;
```

Like functions, make sure your variable names are descriptive, be it globals, fields, or local variables. Only use names like `temp` if its for truly temporary values that are immediately obvious what they do at a glance. Otherwise prefer a name that describes the thing the variable represents. Also like functions, avoid these being overly verbose.

Avoid using the `local` keyword when defining local variables as it's no longer necessary. Avoid prefixes and suffixes if they serve no purpose and avoid putting numbers in your variable names.

Only use `typedef` if it adds a level of clarity and ease to what your date type is doing in your use case. Keep these as local as possible to avoid confusion.