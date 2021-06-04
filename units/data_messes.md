---
title: Identifying Data Messes
date: 2021-06-17
description: |
  How to triage your data for tidying
---

## [Miro whiteboard on Data Messes](https://miro.com/app/board/o9J_lC-HL_A=/)


## Column validity errors

- A column has duplicated values when it is supposed to have unique values
- A column has null/empty values when it is supposed to have a value for every single row

## Semantic mismatch errors

- Values that belong in one column are in another column
- Values that belong in one row are in another
- Entering multiple semantically-different pieces of information into the same column. When in doubt, split it out! It's always easier to have the computer merge data back into one column than to split it out after you've entered it.
- Using an inconsistent strategy for multi-valued cells
  - There are several valid solutions to entering multi-valued fields in a record, but you must pick one and stick with it


## Categorical / controlled columns with misspellings or close-matches



## Date validity errors

- Using inconsistent formatting for dates in different rows
- Using different levels of percision (e.g. year vs. year+month+day) for dates **unless you are using [EDTF]**.
- Having a date that doesn't exist, such as `2021-06-31`, or `1920-02-29`.
  - Note: knowing when to treat a year as a [leap year in the Gregorian calendar is more difficult than you might expect](https://en.wikipedia.org/wiki/Leap_year#Gregorian_calendar). The best way to validate your dates is to use built-in data validation in your spreadsheet or database software.

[EDTF]: {{ site.basurl }}{% link units/data_types.md %}

## The Dreaded Notes Field

It's very useful to have a free-text notes field to capture info for a human reader that isn't otherwise structured into other columns. But watch out for these bad Notes mistakes:


### Putting multiple kinds of notes into one single column

- Mixing in internal editorial notes with other discursive text that you want to be publicly viewable (Those should be in separate columns)
- Relying on a careful style guide to structure the text in your notes field. As soon as you find yourself using a punctuation style guide in a free text field, it's likely that you should be using additional columns.

### Putting notes into non-notes columns

| subject                           |
| --------------------------------- |
| trade;government                  |
| higher education                  |
| anatomy;physical therapy          |
| marketing \[need to verify this\] |
| environmentalism                  |

Ideally, a column contains just one kind of information - be it a string value with a title, or a categorical column that may have multiple values from a controlled vocabulary list. Notes to yourself or to users of your data are distinct pieces of information that belong in their own column. If you often need to qualify data in a particular column (like this example of a `subject` column,) it's best to make an additional column like `subject_notes` so that you know the text in that field hs a note about the subject field for that record, distinguishing it from a note about some other column, or general notes about the record itself that aren't specific to an existing field.

