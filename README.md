# Twee2

Command-line tool to compile Twee-style (.tw, .twine) interactive fiction source files to Twine 2-style (non-Tiddlywiki) output.

Designed for those who preferred the Twee (for Twine 1) approach to source management, because the command-line is awesome, but who want to take advantage of the new features in Twine 2. Note that this is NOT a Twine 1 to Twine 2 converter, although parts of its functionality go some way to achieving this goal.

## Philosophy

(Why does this exist? Where is it going?)

I love the direction that Twine 2 has been going in, in regard to ditching the old Tiddlywiki backend and making it easier than ever for developers to integrate their own CSS and Javascript into their stories. However, as a fan of plain-old text editors and not of IDEs, I'm not so keen on the fact that it's now almost-impossible to develop a Twine adventure from the command-line only (there's no "Twee" equivalent for Twine 2). For my own benefit and enjoyment, I aim to fill that gap. If it helps you too, then that's just a bonus.

Right now Twee2 doesn't even support the diversity of original Twee, and it's possible that it never will. As the need arises, though, I may add additional features that seemed to be 'missing' from Twee, to me.

I'd love to hear your thoughts about the future of this gem.

## Prerequisites

You'll need Ruby. Instructions on easily installing it on MacOS, Windows, and Linux can be found at https://www.ruby-lang.org/en/documentation/installation/.

## Installation

Install using gem

    gem install twee2

## Usage

To see usage examples and fuller instructions (documentation on this page is lacking, but as-yet no documentation is complete):

    twee2

To compile a Twee file into a HTML file using the default format (Harlowe):

    twee2 build inputfile.twee outputfile.html

To use a specific format, e.g. Snowman:

    twee2 build inputfile.twee outputfile.html --format=Snowman

For additional features (e.g. listing known formats, watch-for-changes mode), run twee2 without any parameters.

## Special features

Aside from the regular Twee features, Twee2 provides the following enhancements:

### Multi-file inclusion (super-experimental)

You can combine multiple input files into one via either (or both!) of two different methods:

#### StoryIncludes

Borrowed from Twee: simply list the files to include in the special StoryIncludes passage. Each will be appended to the end of your source file on compilation.

```
::StoryIncludes
my-sub-story.tw2
```

Looking for something more-powerful? Use ::@include-syntax, e.g.:

```
::IncompleteRoom [haml]
%p
  This room is incomplete. Come back later.
:coffeescript
  ::@include incomplete-room-js.coffee
```

The requested file will be nested directly in place. Indent levels will be preserved, which makes it safe for use within HAML, Coffeescript, and SASS. This makes it easy to re-use content throughout your story by simply inserting it in multiple places.

### HAML support

You can declare your passages using [HAML markup](http://haml.info/docs/yardoc/file.REFERENCE.html) by applying a 'haml' tag to the passage, e.g.:

```
::DarkCorridor [haml]
%p
  The floorboards creak beneath your feet as you creep into the darkness of the corridor.
```

### Coffeescript

If you'd rather write your Javascript in [Coffeescript](http://coffeescript.org/) style, just use a HAML ':coffeescript' block or tag your 'script' block with 'coffee':

```
::MyJavascripts [coffee script]
  $ ->
    alert 'Welcome to my game!'
```

### SASS/SCSS stylesheets

Prefer SASS for your stylesheets? Just use a 'sass' or 'scss' tag alongside your 'stylesheet' tag, or use a :sass or :scss block in HAML:

```
::MyStylesheet [scss stylesheet]
body {
  color: #eee;
}
tw-passage {
  tw-link {
    color: red;
  }
}
```

## Notes

* This is not a Twee to Harlowe converter. You'll still need to change your macros as described at http://twine2.neocities.org/, and/or rewrite them as Javascript code.
* Some special story segments (e.g. StorySubtitle) are ignored. You will be warned when this happens.
* The HTML files that are produced by this can not be readily re-opened by Twine 2 (I think it's because of the missing passage coordinate data).
* Seriously: this is very-much an experiment and you probably shouldn't use it.

## License

This code is released under the GPL, version 2. It includes code (in the storyFormats directory) by other authors, including Leon Arnott: please read their licenses before redistributing.