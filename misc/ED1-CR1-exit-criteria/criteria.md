# IMSC HRM ED1 CR1 exit criteria

## Scope

This document specifies the exit criteria for the first CR transition (CR1) of the first edition (ED1) of the IMSC HRM
specification.

## Criteria

As required by the [TTWG charter](https://github.com/w3c/charter-timed-text), the following two independent factors are
used to demonstrate implementation experience:

* at least one implementation of the specification
* content consisting of:
  * synthetic IMSC documents exercising salient features of the HRM model
  * substantial collections of sample IMSC documents from two independent authors

Each IMSC document SHALL be accompanied by an assertion indicating whether the IMSC document is expected to pass or fail
the HRM requirements.

When evaluating an IMSC document, each implementation SHALL confirm the associated assertion, unless the assertion is determined to be in error.

## Features at risk

Unless a substantial and varied corpus of IMSC Image Profile Documents are made available, the portions of the IMSC HRM specification that are specific to IMSC Image Profile Documents will be removed.

## Synthetic tests

The [tests](./tests) directory contains documents designed to exercise salient features of the HRM model.

The table below specifies the assertion for each document.

| Document     | Assertion |
| ------------ | --------- |
| fail001.ttml | Fail      |

## Content tests

To be determined, following a call for test content issued by the Working Group.
