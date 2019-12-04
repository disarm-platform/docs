# Basics of writing a containerised function

Regardless of the language and dependencies, all functions need to use the same basic approach.

* They exist in a _stateless_ container - it has no memory of previous inputs, downloads, results, etc. Imagine it runs fresh, from scratch, every time. There are implications here for required data, etc. But the benefits are that you have a predictable, reproducible and scalable way to respond to requests.
* They will receive and produce JSON, a human-readable text format for describing data.

## `STDIN`, `STDOUT` and JSON

The containerised functions have a very simple way of interacting with the outside world. They assume everything coming in is a stream of characters \(standard input or `STDIN`\), and that all they can return is also a stream of characters \(standard output or `STDOUT`\).

Our templates combined with OpenFaas abstract away most of this, and you can assume that \(depending on the template language\) the function will:

* receive a request object / dictionary / list containing parameters
* need to return something which can be serialised as JSON

