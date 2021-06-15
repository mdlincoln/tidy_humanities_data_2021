---
title: Relational Data Design Exercise
date: 2021-06-15
description: |
  Learning how to design relational data with interlinked tables
---

Goal: to create a data design that can represent the information contained in this catalog of an auction of paintings:

<https://archive.org/details/catalogueofhighl00chri/page/n13/mode/2up>

Working as a group or solo, first select potential goals. Some possibilities include:

1. Track which artists, or nationalities/regions of artists commanded the highest or the lowest prices. (hint: the handwritten three-part numbers represent British sterling, represented as `pounds.shillings.pence`)
2. Identify recurring words or rhetorical strategies used by the auction authors, and whether they are associated with the type of artwork or the nationality of the artist
3. Trace connections between artists made by the catalog authors when, in describing the work of one artist, they mention the name of another.
4. Look for connections between previous owners of an artwork, which are sometimes listed for the more prestigious sale lots. Can we list out which collectors sought out which artists? Can we chart connections between previous owners of the same artwork?

[Go to the Miro Relational Data Diagramming whiteboard](https://miro.com/app/board/o9J_lCqAXCs=/)

With your group, use the "mind map" tool in Miro to build out a data design that represents the sales of artworks in this auction catalog in a way that could help you answer your selected question. (you may need to look in the `...` menu to find it - you can drag it to your toolbar.)

![Miro mind map tool]({{ site.baseurl }}/assets/img/mind_map.png)

1. Entities: each thing (be it a `person`, a `place`, a `concept`, an `object`, etc.) that you want to independently track. Each entity represents a table in your data.
![Entity example]({{ site.baseurl }}/assets/img/entity.png)
2. Attributes: each entity will have attributes - text, categorical, numerical, or date data inherent to that entity. For example, a `person` entity may have `name` and `birth_date` attributes. Each attribute represents a column in that entity's table
![Attributes example]({{ site.baseurl }}/assets/img/attributes.png)
   1. *Every entity must have an `id` attribute* - a unique string or number that represents that entity, and which can be referred to from other tables.
3. Some attributes may point to other entities, such as a person's `active_location` attribute referencing a `Location` entity, that has its own additional attributes. In traditional database parlance, this is called a "foreign key relation".
   ![Attribute relational reference]({{ site.baseurl }}/assets/img/entity_relation.png)

Remember, the goal isn't to actually enter all the data from the auction catalog into tables, but to try and come up with the *set of tables* that could do the job right. That said, do try to test out your data design by creating tables in a shared Google Sheets doc.

Consider Mark Merry's source-oriented <-> method oriented axis of historical database design: will you try to create a data design that will capture every single eccentricity of the original printed and hand-annotated auction catalogue? Or will you make a focused database that only collects the information vital to your chosen goal? As Merry suggests, you will likely choose a middle path.

Although there are certainly better and worse approaches to designing a historical database, **there is no one CORRECT data design** for this exercise. After working out designs individually or in breakout groups, we'll reconvene to share and compare our different solutions.