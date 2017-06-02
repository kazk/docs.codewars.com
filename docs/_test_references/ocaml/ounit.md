---
title: OUnit Testing Framework
language: ocaml

introduction: |-
  Codewars supports [OUnit](http://ounit.forge.ocamlcore.org/api-ounit/) testing framework.

assertions:
  - name: assert_failure
    sig: |-
      val assert_failure : string -> 'a
    id: assert-failure
    desc: |-
      Signals a failure.
      This will raise an exception with the specified string.

  - name: assert_bool
    sig: |-
      val assert_bool : string -> bool -> unit
    id: assert-bool
    desc: |-
      Signals a failure when bool is false.
      The string identifies the failure.

  - name: assert_string
    sig: |-
      val assert_string : string -> unit
    id: assert-string
    desc: |-
      Signals a failure when the string is non-empty.
      The string identifies the failure.

  - name: assert_equal
    sig: |-
      val assert_equal :
        ?ctxt:test_ctxt ->
        ?cmp:('a -> 'a -> bool) ->
        ?printer:('a -> string) ->
        ?pp_diff:(Format.formatter -> 'a * 'a -> unit) ->
        ?msg:string ->
        'a -> 'a -> unit
    id: assert-equal
    desc: |-
      `assert_equal expected real`

      Compares two values, when they are not equal a failure is signaled.

      `ctxt` : if provided, always print expected and real value

      `cmp` : customize function to compare, default is `=`

      `printer` : value printer, don't print value otherwise

      `pp_diff` : if not equal, ask a custom display of the difference using
      `diff fmt exp real` where `fmt` is the formatter to use

      `msg` : custom message to identify the failure

  - name: assert_raises
    sig: |-
      val assert_raises :
        ?msg:string ->
        exn -> (unit -> 'a) -> unit
    desc: |-
      Asserts if the expected exception was raised.

      `msg` : identify the failure

helpers:
  - name: cmp_float
    sig: |-
      val cmp_float : ?epsilon:float -> float -> float -> bool
    id: cmp-float
    desc: |-
      Compare floats up to a given relative error.
      `epsilon`: if the difference is smaller epsilon values are equal

construction:
  - name: '>:'
    sig: |-
      val (>:) : string -> test -> test
    id: label-test
    desc: Create a TestLabel for a test
  - name: '>::'
    sig: |-
      val (>::) : string -> test_fun -> test
    id: label-test-case
    desc: Create a TestLabel for a TestCase
  - name: '>:::'
    sig: |-
      val (>:::) : string -> test list -> test
    id: label-test-list
    desc: Create a TestLabel for a TestList
  - name: test_case
    sig: |-
      val test_case : ?length:test_length -> test_fun -> test
    id: test-case
    desc: Generic function to create a test case.
  - name: test_list
    sig: |-
      val test_list : test list -> test
    id: test-list
    desc: Generic function to create a test list.
---

# OUnit Testing Framework

Codewars supports [OUnit](http://ounit.forge.ocamlcore.org/api-ounit/) testing framework.

## Assertions

{% for a in page.assertions %}
<h3 id="{{ a.id }}">{{ a.name }}</h3>
{% highlight ocaml %}{{ a.sig }}{% endhighlight %}

{{ a.desc | markdownify }}
{% endfor %}


### Example

```ocaml
module Tests = struct
  open OUnit
  let suite = [
    "Person module">:::
     ["test_greet">:: (fun _ ->
       let person : Person.t = { Person.name = "Jack" } in
       assert_equal "Hello, Jack!" (Person.greet person))]];;
end
```

{% comment %}

- <https://www.qualified.io/kb/languages/ocaml/ounit>

{% endcomment %}
