# Sassquatch

### Background

It's TDD for Sass (er, um, SCSS). Yes, you read correctly, it's TDD for SCSS. I'll wait while you sit and stare in disbelief.

#### Wait, what!?

Okay, feel better now? Right now it's just an idea. I mean, it works, but it's not complete. There are two matchers (`equal-to` and `almost-equal-to`), you have to run it with the `sass` command line tool and visually parse the output. Oh yeah, and it only works for functions. And it's 100% pure SCSS code. Hey, this is how these things get started.

#### TDD, Sass, srsly?

As functions and mixins become more complex, the rapid feedback of a TDD cycle becomes a necessity to keep the code clean and minimal. Failing tests will help point out when you broke something you might otherwise have missed, or at least spent hours debugging. Just like regular TDD, 100% coverage should never be your goal. We were not put on this Earth to ensure we correctly specified `background-color: purple`. But it would be useful to know your `to-em` function is still returning the correct values after upgrading Sass.

### What does it look like?

Sassquatch tests are structurally inspired by RSpec:

```scss
the-feature-i-am-testing {
  the-test-i-am-writing {
    expect: matcher(expected, actual);
  }
}
```

So for example, let's say you're testing a function that calculates a grid column width:

```scss
@function grid-width($cols) {
  @return $col-width * $cols - $gutter-width;
}
```

I might have a test stored at `stylesheets/tests/grid-columns.scss` like:

```scss
grid-columns {
  five-columns-at-960px {
    expect: to-equal(grid-width(5), 400px);
  }
}
```

When I run `sass stylesheets/tests/grid-columns.scss` I'd get the output:

```css
grid-columns five-columns-at-960px {
  expect: true;
}
```

Useful, but what if I broke it? Let's say we change our grid size to 1140px. Running the test would output:

```css
grid-columns five-columns-at-960px {
  expect: 95px;
}
```

So instead of true, you now see what your function actually returned. Simple eh?

[Check out the actual example this came out of](https://github.com/d-i/Sassquatch/tree/master/example).

### Interested?

Okay, I know it could be a lot better. But it's a start. To say there's a lot of work to be done is an understatement. We aren't at the point where we can know everything we need to do. But there are a few things that would be nice for this little project:

- Better CLI runner that does some simple parsing of the Sass output
- A way to actually include this in your projects (a generator perhaps?)
- A few more matchers
- A method for testing mixins
- A proper parser for tests

There may be more. If you're into this sort of thing (and, be honest, who the heck isn't?) check out the issues and send a pull request. Feel free to open issues to discuss new features or architectural changes.


Thanks!
The Sassquatch
