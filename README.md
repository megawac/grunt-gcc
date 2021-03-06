# grunt-gcc

[Grunt](http://gruntjs.com/) task for minifying JavaScript files with Google Closure Compiler.

For grunt 0.3, install the latest `0.1.x` version. Grunt 0.4 support starts with version `0.2.0`.

## Installation

```
npm install grunt-gcc
```

Add to `grunt.js`:

```js
grunt.loadNpmTasks('grunt-gcc');
```

`initConfig` task:

```js
gcc: {
	dist: {
		src: ['src/foo.js', 'src/bar.js'],
		dest: 'dist/foobar.min.js'
	}
}
```

## Options

You can pass options with:

```js
gcc: {
	dist: {
		options: {
			compilation_level: 'ADVANCED_OPTIMIZATIONS'
		},
		src: ['src/foo.js', 'src/bar.js'],
		dest: 'dist/foobar.min.js'
	}
}
```

---

### compilation_level:

- `WHITESPACE_ONLY` : Removes comments, line breaks, unnecessary spaces, and other whitespace.
- `SIMPLE_OPTIMIZATIONS` *default* : Previous plus shortens local variables, function names, and function parameters.
- `ADVANCED_OPTIMIZATIONS` : Previous but also for global variables, function names, and function parameters.

For more specific explanation, visit the [Closure Compiler Compilation Levels documentation](https://developers.google.com/closure/compiler/docs/compilation_levels).

---

### banner:

Text banner that will be inserted at the beginning of minified file.

```js
gcc: {
	dist: {
		options: {
			banner: '<%= meta.banner %>'
		},
		src: 'src/foo.js',
		dest: 'dist/foobar.min.js'
	}
}
```

---

### create_source_map:

Pass a path to a source map if you want to create one. The target directory for sourcemap has to exist.

```js
gcc: {
	dist: {
		options: {
			create_source_map: 'dist/foo.min.js.map'
		},
		src: 'src/foo.js',
		dest: 'dist/foo.min.js'
	}
}
```

---

#### Rest of the Closure Compiler options as defined in --help

```
 --charset VAL                          : Input and output charset for all
                                          files. By default, we accept UTF-8 as
                                          input and output US_ASCII
 --compilation_level [WHITESPACE_ONLY   : Specifies the compilation level to
 | SIMPLE_OPTIMIZATIONS | ADVANCED_OPTI : use. Options: WHITESPACE_ONLY,
 MIZATIONS]                             : SIMPLE_OPTIMIZATIONS, ADVANCED_OPTIMIZ
                                          ATIONS
 --compute_phase_ordering               : Runs the compile job many times, then
                                          prints out the best phase ordering
                                          from this run
 --create_name_map_files                : If true, variable renaming and
                                          property renaming map files will be
                                          produced as {binary name}_vars_map.out
                                          and {binary name}_props_map.out. Note
                                          that this flag cannot be used in
                                          conjunction with either variable_map_o
                                          utput_file or property_map_output_file
 --create_source_map VAL                : If specified, a source map file
                                          mapping the generated source files
                                          back to the original source file will
                                          be output to the specified path. The
                                          %outname% placeholder will expand to
                                          the name of the output file that the
                                          source map corresponds to.
 --debug                                : Enable debugging options
 --define (--D, -D) VAL                 : Override the value of a variable
                                          annotated @define. The format is
                                          <name>[=<val>], where <name> is the
                                          name of a @define variable and <val>
                                          is a boolean, number, or a single-quot
                                          ed string that contains no single
                                          quotes. If [=<val>] is omitted, the
                                          variable is marked true
 --externs VAL                          : The file containing javascript
                                          externs. You may specify multiple
 --formatting [PRETTY_PRINT | PRINT_INP : Specifies which formatting options,
 UT_DELIMITER]                          : if any, should be applied to the
                                          output JS. Options: PRETTY_PRINT,
                                          PRINT_INPUT_DELIMITER
 --help                                 : Displays this message
 --js VAL                               : The javascript filename. You may
                                          specify multiple
 --js_output_file VAL                   : Primary output filename. If not
                                          specified, output is written to stdout
 --jscomp_dev_mode (--dev_mode) [OFF |  : Turns on extra sanity checks
 START | START_AND_END | EVERY_PASS]    :
 --jscomp_error VAL                     : Make the named class of warnings an
                                          error. Options:accessControls,
                                          checkRegExp,checkTypes, checkVars,
                                          deprecated, fileoverviewTags,
                                          invalidCasts, missingProperties,
                                          nonStandardJsDocs, strictModuleDepChec
                                          k, undefinedVars, unknownDefines,
                                          visibility
 --jscomp_off VAL                       : Turn off the named class of warnings.
                                          Options:accessControls, checkRegExp,ch
                                          eckTypes, checkVars, deprecated,
                                          fileoverviewTags, invalidCasts,
                                          missingProperties, nonStandardJsDocs,
                                          strictModuleDepCheck, undefinedVars,
                                          unknownDefines, visibility
 --jscomp_warning VAL                   : Make the named class of warnings a
                                          normal warning. Options:accessControls
                                          , checkRegExp,checkTypes, checkVars,
                                          deprecated, fileoverviewTags,
                                          invalidCasts, missingProperties,
                                          nonStandardJsDocs, strictModuleDepChec
                                          k, undefinedVars, unknownDefines,
                                          visibility
 --logging_level VAL                    : The logging level (standard java.util.
                                          logging.Level values) for Compiler
                                          progress. Does not control errors or
                                          warnings for the JavaScript code
                                          under compilation
 --manage_closure_dependencies          : Automatically sort dependencies so
                                          that a file that goog.provides symbol
                                          X will always come before a file that
                                          goog.requires symbol X. If an input
                                          provides symbols, and those symbols
                                          are never required, then that input
                                          will not be included in the compilatio
                                          n.
 --module VAL                           : A javascript module specification.
                                          The format is <name>:<num-js-files>[:[
                                          <dep>,...][:]]]. Module names must be
                                          unique. Each dep is the name of a
                                          module that this module depends on.
                                          Modules must be listed in dependency
                                          order, and js source files must be
                                          listed in the corresponding order.
                                          Where --module flags occur in
                                          relation to --js flags is unimportant
 --module_output_path_prefix VAL        : Prefix for filenames of compiled js
                                          modules. <module-name>.js will be
                                          appended to this prefix. Directories
                                          will be created as needed. Use with
                                          --module
 --module_wrapper VAL                   : An output wrapper for a javascript
                                          module (optional). The format is
                                          <name>:<wrapper>. The module name
                                          must correspond with a module
                                          specified using --module. The wrapper
                                          must contain %s as the code placeholde
                                          r
 --output_manifest VAL                  : Prints out a list of all the files in
                                          the compilation. If --manage_closure_d
                                          ependencies is on, this will not
                                          include files that got dropped
                                          because they were not required. The
                                          %outname% placeholder expands to the
                                          js output file. If you're using
                                          modularization, using %outname% will
                                          create a manifest for each module.
 --output_wrapper VAL                   : Interpolate output into this string
                                          at the place denoted by the marker
                                          token %output%. See --output_wrapper_m
                                          arker
 --output_wrapper_marker VAL            : Use this token as output marker in
                                          the value of --output_wrapper
 --print_ast                            : Prints a dot file describing the
                                          internal abstract syntax tree and
                                          exits
 --print_pass_graph                     : Prints a dot file describing the
                                          passes that will get run and exits
 --print_tree                           : Prints out the parse tree and exits
 --process_closure_primitives           : Processes built-ins from the Closure
                                          library, such as goog.require(),
                                          goog.provide(), and goog.exportSymbol(
                                          )
 --property_map_input_file VAL          : File containing the serialized
                                          version of the property renaming map
                                          produced by a previous compilation
 --property_map_output_file VAL         : File where the serialized version of
                                          the property renaming map produced
                                          should be saved
 --summary_detail_level N               : Controls how detailed the compilation
                                          summary is. Values: 0 (never print
                                          summary), 1 (print summary only if
                                          there are errors or warnings), 2
                                          (print summary if type checking is
                                          on, see --check_types), 3 (always
                                          print summary). The default level is 1
 --third_party                          : Check source validity but do not
                                          enforce Closure style rules and
                                          conventions
 --use_only_custom_externs              : Specifies whether the default externs
                                          should be excluded
 --variable_map_input_file VAL          : File containing the serialized
                                          version of the variable renaming map
                                          produced by a previous compilation
 --variable_map_output_file VAL         : File where the serialized version of
                                          the variable renaming map produced
                                          should be saved
 --version                              : Prints the compiler version to stderr.
 --warning_level [QUIET | DEFAULT |     : Specifies the warning level to use.
 VERBOSE]                               : Options: QUIET, DEFAULT, VERBOSE
```

In options that do not accept value, just pass `true` instead. Also with options that accept multiple values, pass
the values in an array to that option:

```js
gcc: {
	dist: {
		options: {
			debug: true, // Simple flag without input value
			externs: [   // Multiple values
				'jquery.js',
				'underscore.js'
			]
		},
		src: ...,
		dest: ...
	}
}
```