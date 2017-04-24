# Riptide: Problem

[![Rescue Ring](../docs/rescue-ring.jpg)](https://pixabay.com/en/lifesaver-life-buoy-safety-rescue-933560/)

[![Build Status](https://img.shields.io/travis/zalando/riptide.svg)](https://travis-ci.org/zalando/riptide)
[![Coverage Status](https://img.shields.io/coveralls/zalando/riptide.svg)](https://coveralls.io/r/zalando/riptide)
[![Javadoc](https://javadoc-emblem.rhcloud.com/doc/org.zalando/riptide-problem/badge.svg)](http://www.javadoc.io/doc/org.zalando/riptide-problem)
[![Release](https://img.shields.io/github/release/zalando/riptide.svg)](https://github.com/zalando/riptide/releases)
[![Maven Central](https://img.shields.io/maven-central/v/org.zalando/riptide-problem.svg)](https://maven-badges.herokuapp.com/maven-central/org.zalando/riptide-problem)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/zalando/riptide/master/LICENSE)

*Riptide: Problem* adds [`application/problem+json`](https://tools.ietf.org/html/rfc7807) support to *Riptide* using 
[zalando/problem](https://github.com/zalando/problem).

## Example

```java
http.post("/").dispatch(series(),
    on(SUCCESSFUL).call(pass()),
    anySeries().call(problemHandling()));
```

## Features

- reusable
- content negotiation
- problem propagation

## Dependencies

- Java 8
- Riptide: Core
- Problem

## Installation

Add the following dependency to your project:

```xml
<dependency>
    <groupId>org.zalando</groupId>
    <artifactId>riptide-problem</artifactId>
    <version>${riptide.version}</version>
</dependency>
```

## Usage

If a problem is being received it will be mapped to a
[`ThrowableProblem`/`Exceptional`](https://github.com/zalando/problem#throwing-problems). It can be inspected as the
cause of the `CompletionException`:

```java
import static org.zalando.riptide.problem.ProblemRoute.problemHandling;

try {
    http.post("/").dispatch(series(),
        on(SUCCESSFUL).call(pass()),
        anySeries().call(problemHandling()))
        .join();
} catch (CompletionException e) {
    assert e.getCause() instanceof Problem; // TODO handle
}
```

## Getting Help

If you have questions, concerns, bug reports, etc., please file an issue in this repository's [Issue Tracker](../../../../issues).

## Getting Involved/Contributing

To contribute, simply make a pull request and add a brief description (1-2 sentences) of your addition or change. For
more details, check the [contribution guidelines](../CONTRIBUTING.md).