---
title: Data types
sequence: 2
date: 2021-06-15
description: |
  Strings, categories, numbers, units
---

* TOC
{:toc}

## Sample data: [Artworks depicting Amsterdam](https://docs.google.com/spreadsheets/d/1P7or2IH0FZG0UsqHJRt71L3I8Ptxc80rxE7bai7ecUA/edit#gid=1462177897)

## Numbers

- Counting vs. measuring
  - A column that represents a count should always be a positive integer
  - A column representing a measurement may have decimals (often referred to as a "real" number, or a "float" in some database software) and may be negative
- Dealing with units and dimensions
  - If it is important for you to be able to filter & sort these measurements (and not just store them to read later) then you should endeavor to have consistent units and record each dimension in a separate column.

## Text

- Short texts vs. long/complex text
  - Most spreadsheet software can properly store relatively large amounts of text in individual cells and export it correctly to a CSV file. However if you have particularly long texts, like the full texts of an article or book, it is advisable to save the full text of each individual work to its own file with a unique filename, and put that filename into your tables instead. This way, you can store and update the data *about* that text independently from the long text itself. This is a common data management practice for text analysis projects.
- Character encodings
  - [Character encodings are a complicated topic](https://www.w3.org/International/questions/qa-what-is-encoding), but they are generally to blame when you open up someone else's data in your spreadsheet program of choice, and the characters (particularly characters with accents or non-Latin characters) appear garbled. This is because the other person saved their data using one character encoding, and your program tried to open it with a different encoding.
  - By in large, when making and saving your own data, you should save it as UTF-8, an encoding that handles a wide range of non-Latin characters. Google Sheets will do this for you; Microsoft Excel will still often try to save it using older encodings that can mangle your text. When exporting to CSV, always make sure to select UTF-8 as your encoding.

## Categories

- "text that isn't just text" - keep your categorical data standardized (often referred to as a "controlled" field)
- Important for any column that you would want to filter or count on.
- when do my categories need to have their own separate table?
  - When the categories have attributes other than a name/label
  - When categories might be shared attributes between several different tables (e.g. if you have a `Books` table and a `Buildings` table, `Books:Publication Place` and `Buildings:Location` might both reference a common vocabulary of `Locations`.)
  - When using data validation on Google Sheets or Excel, you can require entries in a cell to match one of a pre-set list of values in another range/table

## Multiple values

Several different approaches:

- Use a single column with a special character delimiter
  - Pros: simple to enter and allows a flexible number of values.
  - Cons: requires that your processing software can handle multi-valued fields with delimiters \[OpenRefine and Palladio both can do this\]; the multiple values cannot structure complex information.
- Use multiple, numbered columns
  - Pros: simple to enter data without typos; very clear how to handle the data (`author1`, `author2`, etc.); Easier to set up data validation within spreadsheet programs like Google Sheets or Excel.
  - Cons: you need to pre-determine the number of possible values at the start; extra processing required later on if you want to filter or count the values across those columns
- Use a linked table to describe the relationships
  - Pros: handles one-to-many or many-to-many relationships between entities; lets you add additional attributes to each relationship, such as adding relationship types or durations to a person's relationships to other people; allows a flexible number of values; a common solution in database software.
  - Cons: must maintain additional tables; use joins or `VLOOKUP` in Excel/Google Sheets to process the data; Difficult to maintain data validity without a true relational database.

## Missing data

- If you intend to filter, count, or do other computing with a table based on a certain column, every value in that column must represent a specific instance of the thing to be counted (such as a person, a location, a concept.) If you put `ANONYMOUS` into an `author` column, any analytical process will count that as a single actual person! Alternatives:
  - If all you need to record is the absence of information, then leave the cell blank
  - For certain kinds of analyses like network analysis, you may need to artificially create individual unidentified entities, like `anonymous1`, `anonymous2` etc. The benefit of this is it allows you to add attributes about entities that aren't uniquely identified but about which we know some things. For example, you could have a table of all your people, with `anonymous827` having an assumed nationality of `German` and a rough range of active dates.

## Uncertain data

Think very carefully before you endeavor to encode uncertainty into your data. Like most computing tasks, it is entirely possible, but may require more labor than you realize:

- Consider how you will use information about uncertainty
  - Do you want to filter, count, or compute fields based on a set uncertainty scale? In that case, you will need a controlled vocabulary.
  - Do you only want to mark uncertainty for a human readable note, but otherwise be able to have someone find the record when filtering for a given uncertain value? (e.g. searching for all works associated by Rembrandt, and seeing that some of the items have complex qualifications to their attributions in the notes) In that case, maintaining a free text field is fine.
- If you must use an uncertainty vocabulary, consider carefully how you will communicate it to your audience / data re-users / yourself 12 months from now.
  - Avoid numeric uncertainty scales: different readers will interpret the same number very differently.
  - Use as small and concrete a vocabulary as possible. If it takes you more than a few seconds to judge and enter the uncertainty in a record, than you are not dealing with usefully categorizable uncertainty. You won't be able to usefully query it if the vocabulary is too rich and ambiguous, and so you might as well just have a non-controlled notes field about it.

## Dates

- [LEARN AND USE **EDTF** WHENEVER POSSIBLE](https://miro.com/app/board/o9J_l_LUDX4=/) It handles many needs in a way that computers can read:
  - dates with varying precision (`1970`, `1991-01`, `2021-04-06`)
  - dates that are approximate (`1970~`) or uncertain (`1970?`)
  - date ranges (`1980/2010`)
  - There are [easy tools](https://matthewlincoln.net/pages/edtf.html) that convert EDTF dates into precise date ranges used by most software, allowing you to create an `earliest_date` and `latest_date` column for most EDTF strings.
- Consider whether you are recording single dates vs. temporal periods with both a start & end date.
