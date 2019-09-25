# Philosophy

Margin is a lightweight markup language for heirarchically structured thought, like notes and to-do lists.

Its platform-independent structure is both human and machine readable.

This means that Margin can thrive within any plain text editor, and on any hardware -- even paper.

However unpredictably a thinker prefers to indent, ornament, number, or label their text, Margin will interpret their [**items**](#items) predictably:

```margin
Favorite Movies
   Eyes Wide Shut
   Black Narcissus
   Adaptation

[Is equivalent to...]

** Favorite Movies: **
  - Eyes Wide Shut
  - Black Narcissus
  - Adaptation

[Is equivalent to...]

__Favorite Movies__
    * Eyes Wide Shut
    * Black Narcissus
    * Adaptation
```

This allows the thinker to adopt whatever visual grammar they prefer.

Items can also be assigned arbitrary [**annotations**](#annotations), which can store meta-data:

```margin
Favorite Movies
   Eyes Wide Shut [year: 1999]
   Black Narcissus [year: 1947]
   Adaptation [year: 2002]
```

Annotations can also signal how items should be interpreted, eg. as tasks:

```margin
Movies to watch:
   [x] Shoplifters
   [ ] Lawrence of Arabia
   [ ] Inland Empire
```

Margin is especially useful for applications that wish to be less prescriptive in their mental models, leaving it to the user to determine how they'd like to interpret the heirarchical structure. 

Margin aims to shepherd apps away from the tendency to overcomplicate and over-define.


### Points of frustration that led to Margin {docsify-ignore}

There are plenty of well-known, powerful applications that force their own organizational philosophy onto the user. And there's nothing inherently wrong with that.

Nevertheless, when an application's user-facing models of thought...
  1. cannot be easily mapped to the the user's own mental models, or
  2. are not justified for the user,

it can lead to frustration. For example:
- A mobile to-do list app employs a `Flagged` button that takes up valuable home screen space before any tasks have been flagged -- and without knowing whether the user intends to use the flag feature at all. (iOS 13 Reminders)

- A task management app employs a model of Board -> List -> Card. Lists cannot contain other lists, cards cannot contain other cards, cards cannot contain lists, and so on. (Trello)

- A to-do list app dictates a set of reserved attributes, like `Labels` and `Filters`, which cannot be removed from the interface. (Todoist)

I use and love all of the above applications. Their specialization is their strength. Margin's philosophy simply asserts that there is space for a more adaptable standard for stuctured thought.

In this respect, Margin promotes a common sense approach to modeling thought: simply place the thinker's preferences first. 

This approach begins with a flexible plain text standard. After that, it is the application's job improve the thinker's experience through specialized tools and prescriptive user-facing models -- as long as the underlying source material remains portable and human-readable.

Margin is free and open-source.

-------------------------------

# Syntax

Margin employs an ordered tree data structure whose nodes are called items. Indentation forms the basis of the syntax.

!> To view this document in well-structured Margin, click here (not yet implemented).

## Items

Each line represents an item.

```margin
Shirt
Pants
Shoes
```
Each item can have a single parent, and multiple children. Indentation alone determines this hierarchy:
```margin
Shirt
  Collar
  Sleeves
  Buttons
Pants
  Pant Legs
  Pockets
Shoes
  Tongue
  Laces
```
Leading & trailing dashes, colons, asterisks, chevrons, underscores and whitespaces, as well as blank lines, are ignored:
```margin
    ** Key Takeaways **
    -------------------
       Feel free to use plain text decorations freely in order to:
         - Help structure your thinking
         - Make your plain text documents more easily scannable
```

## Annotations

An annotation is any childless item wrapped in square brackets:
```margin
I'm a plain old item 
   [and I'm an annotation]
```
Annotations can be used to store meta data:
```margin
The Crying of Lot 49
   [author: Thomas Pynchon]
   [publication year: 1966]
   [publisher: J. B. Lippincott & Co.]
```
An annotation is the child of any inline, non-annotation item. If no such item exists, an annotation is the child of the preceding non-annotation item:
```margin
Items:
  - Item A
  - [I belong to Item B] Item B [I also belong to Item B]
  - Item C
  [I belong to Item C]
```
Escape an annotation with a backslash
```margin
This is an item \[but this is not an annotation]
```
Any text up until the (optional) first colon in an annotation may safely be interpreted as the annotation type.

Annotations with type `population`:
```margin
Continents
   Asia          [population: 4,601,371,198]
   Africa        [population: 1,308,064,195]
   Europe        [population: 747,182,751]
   South America [population: 427,199,446]
   North America [population: 366,600,964]
   Oceania       [population: 42,128,035]
```
Annotations with types `waiter` and `host`:
```margin
Restaurant Staff
  Christine [waiter]
  Steven [waiter]
  Jessica [host]
```
An annotation whose type is not understood by the interpreting application may safely be ignored.
```margin
[For example: this annotation won't be utilized unless the app has an interpreter for type "For example".]
```
An annotation cannot be nested 
```margin
[This entire sentence [including this text] represents a single annotation]
```

## Interpreting Items

While there are no hard-and-fast rules about how items should be interpreted, the following are good guidelines for most applications.

### Tasks
A task is any item that parents an annotation of type `x` or `empty string`.
```margin
Daily Rituals
  [x] Meditate
  [ ] Work Out
  [ ] Read for 10 minutes
```

### Indexes
An index is any item that parents an annotation of type `filter`:
```margin
Now Playing [filter: release date is before today]
Coming Soon [filter: release date is after today]
```
An application may use the specified query to filter for certain nodes under certain conditions of interaction. For most applications, the default filter for a given task (when no filter is specified) would be that task's children. But this is outside the scope of the markup language itself.


# Examples

## Note Taking
```margin
-- 'Typography That Works' --
     * Course Notes *
       - Graphic design is all about lining things up (often in a grid)
          Standard Alignments:
           * Centered: Formal, symmetrical
           * Justified: Economical, saves space
           * Flush Left: Organic feeling
           * Flush Right: Unusual, lends a dynamism
       - There should be a self-contained logic to the chosen grid
       - Multiple ideas should be tested rapidly before layout decisions are made
  
     * Assignments *
       - Project 1 [due: 2019/01/12]
       - Midterm [due: 2019/02/18]
       - Final Project [due: 2019/03/14]
```

## To-Do List

```margin
Today       [filter: date is today]
Next 7 days [filter: date is less than 7 days from today]

------

To Do:

  ** Shopping **
    [x] Groceries
    [x] Milk
    [x] Kale
    [ ] Frozen Fish [Note: Any sort of white fish, not cod]

  ** Projects **
    Portfolio Website
      Front-end
        [ ] Disallow zoom on mobile
        [ ] Fix homepage grid on mobile
      Back-end
        - Wordpress
          [ ] Update plugins   [date: 2019/07/07]
        - Server
          [ ] Renew hosting    [date: 2020/01/07]
          [ ] Upgrade to PHP 7 [date: 2020/02/14]
        
```


# Questions

**Why not TaskPaper?**

[TaskPaper](https://www.taskpaper.com) is a great, minimal app for creating to-do lists. Some readers might feel that Margin's capabilities are redundant, but I believe Margin stands apart in several key ways:

- Margin is not an app, but a markup language.
- Margin is heirarchically less prescriptive than TaskPaper. Where TaskPaper splits items into `projects`, `tasks`, and `notes`, Margin sees only items. A top-level item in Margin *could* be considered a project, but it could also just as easily be considered a list, a note, a task, a chapter, an employee, an index, etc. 
- Margin is syntactically less prescriptive than [TaskPaper's formatting](https://guide.taskpaper.com/getting-started/). TaskPaper categorizes items by their ornamentation (`projects` end with a colon, `tasks` begin with a dash, and `notes` must not fall into either of those two categories). Margin intentionally avoids such definitions, allowing the user to ornament (or not) plain text in nearly any format they prefer.
