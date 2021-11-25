# IMSC Hypothetical Render Model (HRM)

* Status: [First Public Working Draft](https://www.w3.org/TR/2021/WD-imsc-hrm-20211109/)
* Participate: [Timed Text Working Group](https://www.w3.org/groups/wg/timed-text)
* Issue Tracker: https://github.com/w3c/imsc-hrm/

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

## User research

The HRM was included in the IMSC Recommendation based on market research conducted in the context of its predecessor specification
(CFF-TT). This research demonstrated that, unless constrained in complexity, a syntactically valid IMSC document could not be
guaranteed to be reliably rendered on all client devices since they do not share identical computing power. For example, a
television typically has a fraction of the computing power available to a desktop PC.

More recently, experience deploying IMSC in ATSC 3.0 systems demonstrated that, in absence of an HRM, it is trivial to convert
legacy [CEA 608/708 captions](https://en.wikipedia.org/wiki/EIA-608) to IMSC documents whose complexity exceed the capabilities of
client devices.

## Design

The HRM specifies an (hypothetical) time required for painting subtitles and captions. Painting includes drawing region backgrounds,
rendering and copying glyphs, and decoding and copying images. Complexity is then limited by requiring that the time to paint a
subtitle/caption is shorter than the time elapsed since the previous subtitle/caption.

The calculation of the time required for painting subtitles and captions is based on a static analysis of the IMSC document and
requires no fetching of external resources or glyph rendering. It is not intended to be an accurate calculation of rendering time,
but a proxy of document complexity.

## Stakeholder Feedback

Stakeholder interest has resulted in the creation of an [open source implementation of the HRM](https://github.com/sandflow/imscHRM).

## Accessibility, Privacy and Security

The purpose of this work is to enable content providers to maximise the chance that their captions and subtitles function as
designed, improving the accessibility of the media supply chain as a whole. The HRM does not specify any human-targeted outputs
and therefore has no direct accessibility implications in itself.

Since the HRM defines the static analysis of a resource, with no specified information flowing to any origin server during the
analysis, there are no direct implications or concerns regarding privacy and security.

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
