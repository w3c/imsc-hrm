# IMSC Hypothetical Render Model (HRM)

* [Latest published version](https://www.w3.org/TR/imsc-hrm/)
* Participate: [Timed Text Working Group](https://www.w3.org/groups/wg/timed-text)
* [Issue Tracker](https://github.com/w3c/imsc-hrm/)
* [Explainer](misc/explainer.md)

## Introduction

The [IMSC Hypothetical Render Model (HRM)](https://www.w3.org/TR/imsc-hrm/) constrains the processing complexity of subtitle and
caption documents that conform to the [IMSC Recommendation](https://www.w3.org/TR/ttml-imsc/).

The HRM is not a new concept: it has been included in all versions and editions of the IMSC Recommendation and has remained
substantially unchanged.

In order to simplify future maintenance, the TTWG wishes to refactor the HRM into its own
[Recommendation](https://www.w3.org/TR/imsc-hrm/).

## Goals

The objecive of the HRM is to allow subtitle and caption authors and providers to verify that the content they provide does not
exceed defined complexity levels, so that playback systems can render the content synchronised with the author-specified display
times.

## Non-goals

The HRM does not specify:

* document syntax, semantics and processing, which are specified in IMSC and its parent [TTML2
  Recommendation](https://www.w3.org/TR/ttml2/);
* editorial requirements, e.g. subtitle and caption reading rates; and
* how IMSC processors and renderers are implemented.

## Design

The HRM specifies an (hypothetical) time required for painting subtitles and captions. Painting includes drawing region backgrounds,
rendering and copying glyphs, and decoding and copying images. Complexity is then limited by requiring that the time to paint a
subtitle/caption is shorter than the time elapsed since the previous subtitle/caption.

The calculation of the time required for painting subtitles and captions is based on a static analysis of the IMSC document and
requires no fetching of external resources or glyph rendering. It is not intended to be an accurate calculation of rendering time,
but a proxy of document complexity.

## Implementation

An open source implementation of the HRM is available at:

[https://github.com/sandflow/imscHRM](https://github.com/sandflow/imscHRM)

## Example

```
<?xml version="1.0" encoding="UTF-8"?>
<tt xml:lang="en"
    xmlns="http://www.w3.org/ns/ttml"
    xmlns:tts="http://www.w3.org/ns/ttml#styling">
  <head>
    <layout>
      <region xml:id="r1" tts:extent="100% 100%"/>
    </layout>
  </head>
  <body region="r1">
    <div>
      <p begin="0s" end="1s">
        <span>hello</span>
      </p>
      <p begin="1s" end="2s" xml:lang="fr">
        <span>bonjour bonjour</span>
      </p>
    </div>
  </body>
</tt>
```

For the first subtitle (_hello_):

    rendering time = time to render {"h", "e", "l", "o"} + time to copy {"l"}
                   = 1/15 * 1/15 * (4 / 1.2 + 1 / 12)
                   = 0.0152s

For the second subtitle (_bonjour bonjour_):

    rendering time = time to clear the screen + time to render {"b", "n", "j", "u", "r", " "}
                        + time to copy {"o", "o", "b", "o", "n", "j", "o", "u", "r"}
                   = 1/12 + 1/15 * 1/15 * (6 / 1.2 + 9 / 12)
                   = 0.1089s

The document above passes the HRM since:

* the rendering time of the first subtitle (0.0152s) is less than 1s, which is the maximum rendering time for the first subtitle in a sequence; and
* the rendering time of the second subtitle (0.1089s) is less than the duration of the first subtitle (1s).
