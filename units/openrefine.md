---
title: OpenRefine Exercise
date: 2021-06-16
description: |
  Working through the Programming Historian's OpenRefine tutorial
---

## [OpenRefine Tutorial](https://doi.org/10.46430/phen0023)

Tips on following the tutorial:

1. **Make sure to import the data properly according to the tutorial instructions** - they walk you through adjusting some of the default import settings to read the data correctly. If you miss this, then a lot of the following steps will give very different results than are shown in the tutorial.
2. Remember to click the "Remove All" button under the "Facet / Filter" menu between steps. This doesn't remove data, it just removes the facet view, letting you start fresh with the next step in the tutorial.
3. While the `Split multi-valued cells...` command is crucial for many data cleaning operations in OpenRefine, remember to `Join multi-valued cells...` again before exporting a CSV of your tidied data.

## Looking for more?

This tutorial only covers a small portion of what OpenRefine can do. A more complete tutorial is available from [Library Carpentry](https://librarycarpentry.org/lc-open-refine/) that you can start to look through if you have time.

I recommend experimenting with the [Knoedler data we used for the Palladio exercise](/mapping-knoedler-palladio/nyc_knoedler.csv) to reconcile the terms to a controlled vocabulary. Reconciliation is the process of linking your own internal lists of people, places, and concepts, to widely-used authorities such as the Library of Congress Subject Headings, the Virtual Internet Authority File, or the Getty Vocabularies. This makes your data more re-usable by others because they can match your exact authority IDs rather than having to parse your text labels for those different entities.

1. Load the Knoelder data into OpenRefine.
2. Split the `genre` column, which uses semicolons `;` as a delimiter
3. Click on the menu for the `genre` column, and select **Reconcile > Start reconciling...**
4. Click the **Add Standard Service...** button, and paste this url in to the box: `https://services.getty.edu/vocab/reconcile` Then click **Add Service**
5. Select the "Getty Vocabularies Reconciliation Service" that should now appear in the menu.
6. Choose to reconcile the cells to the **AAT search**, and then click **Start Reconciling** which will compare the terms in the `genre` column to the Getty's Art & Architecture Thesaurus.
7. After a short wait, you should see options underneath each value. Mouse over each term to see the full definition from the Getty. Once you find the appropriate term to reconcile to, click the double-check-mark box that will match that term to every cell that has the same value. If you don't see an appropriate term, click the double-check-box by **Create new item** which will mark records with that term as not having a reconcilable match. (Note: because of some eccentricities with the way that the Getty's reconciliation service currently works, some of the more general terms like `Landscape` don't get reconciled properly right now.)
8. Continue down the list, and take advantage of the facets that have been created during reconciliation, selecting `none` from the `genre: judgment` facet to show only those records that haven't been reconciled yet.
9. Once you have reconciled the terms, you can use the dropdown menu to choose **Reconcile > Add entity identifiers column** to add a column with the unique identifier for that term from the AAT.


