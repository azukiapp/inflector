## Inflector ##

Rails’ ActiveSupport package includes an inflector class. This lets you do things like singularize and pluralize strings, camel case text, etc.

I’m building a framework that lets Rails developers use erlang + mnesia to replace their ruby models and traditional relational DBs (using Hyperactive Resource + Mochiweb). But a key part of interoperating with rails is being able to infer that “Person” is the singular for “People”.

Inflector brings this magic to erlang! Witness the awesome power:

```erlang
1> inflector:singularize("mice").
"mouse"
2> inflector:titleize("i_love_erlang").
"I Love Erlang"
3> inflector:ordinalize(142).
"142nd"
5> inflector:pluralize("quiz").
"quizzes"
7> inflector:tableize("MyModelModule").
"my_model_modules"
```

Inflector includes functions for pluralizing, singularizing, camelizing, titleizing, capitalizing, humanizing, underscoring, dasherizing, tableizing, moduleizing, foreign_key..isizing? and ordinalizing!

I found it very difficult to implement some functions without regular expressions, so it does require R12B4 of erlang due to the vastly improved regular expression support B4 offers. The majority of the inflections are just standard pattern matching and list manipulation, though.

Also, in order to minimize the impact of compiling the regular expressions, Inflector.erl caches all compiled regular expressions.. so I expect performance won’t be a problem but be aware that it does register a process named “re_cache”.

## Test ##

```sh
$ rebar compile eunit
==> inflector (compile)
Compiled src/inflector.erl
==> inflector (eunit)
Compiled src/inflector.erl
  All 15 tests passed.
Cover analysis: /Users/nuxlli/Work/azuki/inflector/.eunit/index.html
```

## License ##

Copyright 2008 Luke Galea - released under MIT License