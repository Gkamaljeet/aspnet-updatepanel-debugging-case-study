# ASP.NET UpdatePanel Debugging – DOM Duplication Case Study

## Problem
In an ASP.NET WebForms application using UpdatePanel, UI controls and a datetime picker appeared duplicated after async postbacks. Disabling JavaScript removed the issue, indicating a client-side rendering conflict.

## Symptoms
- Entire sections of the page rendered twice
- JavaScript plugins initialized multiple times
- No duplicate script loading
- No console errors

## Investigation
- Verified scripts loaded once via Network tab
- Used MutationObserver to observe DOM changes during async postbacks
- Disabled UpdatePanel to inspect raw HTML output
- Identified unexpected wrapper markup inside UpdatePanel content

## Root Cause
Malformed HTML structure inside the UpdatePanel ContentTemplate caused DOM nesting during partial rendering instead of replacement.

## Resolution
- Removed redundant wrapper markup
- Restored UpdatePanel
- Ensured stable DOM replacement on async postbacks

## Key Learnings
- UpdatePanel replaces inner HTML, not the container
- Invalid markup breaks partial rendering
- Not all UI duplication is caused by JavaScript
- Understanding lifecycle beats quick fixes

## Disclaimer
This repository contains no proprietary or production code. It documents a debugging approach and learning outcome.
