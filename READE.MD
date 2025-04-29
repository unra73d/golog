# Go Simple Logger

[![Go Report Card](https://goreportcard.com/badge/github.com/unra73d/go-log)](https://goreportcard.com/report/github.com/unra73d/go-log)
[![GoDoc](https://godoc.org/github.com/your_username/your_repository_name?status.svg)](https://godoc.org/github.com/unra73d/go-log)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A straightforward, leveled logging package for Go applications featuring global and instance-level controls, tagging, and integrated error checking with optional panic behavior.

## Overview

This package provides a simple logging facility with three levels: DEBUG, WARN, and ERROR. It allows developers to:

*   Control log output globally via package-level constants.
*   Create tagged logger instances (e.g., `[Database]`, `[Network]`) with their own level controls.
*   Easily check errors and log them as warnings or errors.
*   Optionally panic on critical errors using `CheckE` for a fail-fast approach.
*   Recover from panics gracefully within specific function scopes using `BreakOnError`.

The primary goal is to offer a lightweight logging solution that is easy to configure and use, particularly in applications where distinct components benefit from tagged log output.

## Features

*   **Leveled Logging:** Supports DEBUG, WARN, and ERROR levels.
*   **Global Configuration:** Enable/disable log levels globally using `log.DEBUG`, `log.WARN`, `log.ERROR` constants.
*   **Tagged Logger Instances:** Create `logger` instances with specific tags (`log.Logger("MyTag", ...)`).
*   **Instance-Level Configuration:** Enable/disable levels independently for each tagged logger instance.
*   **Combined Control:** Log messages from tagged instances are only printed if *both* the instance flag and the corresponding global flag are enabled.
*   **Error Checking Helpers:**
    *   `CheckW`: Checks an error, logs it as a warning if non-nil, and returns `true` if an error occurred.
    *   `CheckE`: Checks an error, logs it as an error if non-nil (and enabled), and **panics**.
    *   `CheckMultiE`: Checks a slice of errors, logs all non-nil errors (if enabled), and **panics** with the *first* non-nil error found.
*   **Panic Recovery:** Use `defer log.BreakOnError()` (or `loggerInstance.BreakOnError()`) to catch panics triggered by `CheckE`/`CheckMultiE`, log them, and prevent application termination.

## Installation

```bash
go get github.com/unra73d/go-log/log