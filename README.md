<img src="https://github.com/pact-foundation/pact-logo/blob/master/media/logo-black.png" width="200">

# How to get started writing a Pact implementation
1. Read the rest of this file.
2. Read the [implementation guidelines](/implementation-guidelines/README.md)
3. Join the [pact-dev](https://groups.google.com/forum/#!forum/pact-dev) Google group and let people know what you'd like to do and find out if someone has already started work on anything similar.
4. Do it! Ensure your implementation passes all the tests in the testcases directory of the appropriate branch. Start with [version-1](https://github.com/pact-foundation/pact-specification/tree/version-1/testcases) and get that out and battle test it. Then, try for versions 2 and 3.

# Introduction

["Pact"](https://github.com/pact-foundation/pact) is an implementation of "consumer driven contract" testing that allows mocking of responses in the consumer codebase, and verification of the interactions in the provider codebase. The initial implementation was written in Ruby for Rack apps, however a consumer and provider may be implemented in different programming languages, so the "mocking" and the "verifying" steps would be best supported by libraries in their respective project's native languages. Given that the pact file is written in JSON, it should be straightforward to implement a pact library in any language, however, to get the best experience and most reliability of out mixing pact libraries, the matching logic for the requests and responses needs to be identical. There is little confidence to be gained in having your pacts "pass" if the logic used to verify a "pass" is inconsistent between implementations.

To support consistency of matching logic, this specification has been developed as a benchmark that all pact libraries can check themselves against if they want to ensure consistency with other pact libraries.

### Pact Specificaton Philosophy

The Pact matching rules follow [Postel's Law][postel].

* Be as strict as we reasonably can with what we send out (requests). We should know and be able to control exactly what a consumer is sending out. Information should not be allowed to "leak" silently.
* Be as loose as we reasonably can with what we accept (responses). A provider should be able to send extra information that this particular consumer does not care about, without breaking this consumer.
* When writing the matching rules, err on the side of being more strict now, because it will break fewer things to be looser later, than to get stricter later.

Note: One implications of this philosophy is that you cannot verify, using pact, that a key or a header will _not_ be present in a response. You can only verify what _is_.

### Goals for implementing a pact library
* The DSLs should be as similar as possible, within the idioms of the language, to the original Ruby wording to help create a consistent Pact experience, and minimise overhead when switching between languages.
* The matching logic for the requests and responses should be the same so that we can have the same amount of confidence that the integrations will work in real life no matter what language the system was written and tested in.


# Index

* [JSON schemas](https://bitbucket.org/atlassian/pact-json-schema)

* [Version 1](https://github.com/pact-foundation/pact-specification/tree/version-1) - A spec that describes the existing matching in the ruby implementation, and provides test cases for implementations in other languages to ensure that matching is consistent.

* [Version 1.1](https://github.com/pact-foundation/pact-specification/tree/version-1.1) - Updated specification shared between Ruby, JVM and .Net versions.

* [Version 2](https://github.com/pact-foundation/pact-specification/tree/version-2) - Introduces non-language specific regular expression and type matching.

* [Version 3](https://github.com/pact-foundation/pact-specification/tree/version-3) - Introduces pact format for message queues and corrects some issues with V2.

* [Version 4](https://github.com/pact-foundation/pact-specification/tree/version-4) - WIP - Left over candidates from V3.

[postel]: http://en.wikipedia.org/wiki/Jon_Postel#Postel.27s_Law
