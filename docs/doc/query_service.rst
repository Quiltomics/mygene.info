Gene query service
******************************

.. role:: raw-html(raw)
   :format: html
.. |info| image:: /_static/information.png
             :alt: information!


This page describes the reference for MyGene.info gene query web service. It's also recommended to try it live on our `interactive API page <http://mygene.info/v2/api>`_.


Service endpoint
=================

::

    http://mygene.info/v2/query

GET request
==================

Query parameters
-----------------

q
"""""
    Required, passing user query. The detailed query syntax for parameter "**q**" we explained [below](#query-syntax)

fields
""""""
    Optional, can be a comma-separated fields to limit the fields returned from the matching gene hits. The supported field names can be found from any gene object (e.g. `gene 1017 <http://mygene.info/v2/gene/1017>`_). Note that it supports dot notation as well, e.g., you can pass "refseq.rna". If "fields=all", all available fields will be returned. Default:
    "symbol,name,taxid,entrezgene,ensemblgene".

species
"""""""
    Optional, can be used to limit the gene hits from given species. You can use "common names" for nine common species (human, mouse, rat, fruitfly, nematode, zebrafish, thale-cress, frog and pig). All other species, you can provide their taxonomy ids. See `more details here <data.html#species>`_. Multiple species can be passed using comma as a separator. Default: human,mouse,rat.

size
""""
    Optional, the maximum number of matching gene hits to return (with a cap of 1000 at the moment). Default: 10.

from
""""
    Optional, the number of matching gene hits to skip, starting from 0. Default: 0

.. Hint:: The combination of "**size**" and "**from**" parameters can be used to get paging for large query:

::

    q=cdk*&size=50                     first 50 hits
    q=cdk*&size=50&from=50             the next 50 hits

sort
""""
    Optional, the comma-separated fields to sort on. Prefix with "-" for descending order, otherwise in ascending order. Default: sort by matching scores in decending order.


callback
""""""""
    Optional, you can pass a "**callback**" parameter to make a `JSONP <http://ajaxian.com/archives/jsonp-json-with-padding>`_ call.

filter
""""""
    Alias for "fields" parameter.

limit
"""""
    Alias for "size" parameter.

skip
""""
    Alias for "from" parameter.


Query syntax
------------
Examples of query parameter "**q**":


Simple queries
""""""""""""""

search for everything::

    q=cdk2                              search for any fields
    q=tumor suppressor                  default as "AND" for all query terms
    q="cyclin-dependent kinase"         search for the phrase



Fielded queries
"""""""""""""""
::

    q=entrezgene:1017
    q=symbol:cdk2
    q=refseq:NM_001798


.. _available_fields:

Available fields
^^^^^^^^^^^^^^^^
========================    =============================================    =================================================================================
Field                        Description                                     Examples
========================    =============================================    =================================================================================
**entrezgene**                Entrez gene id                                    `q=entrezgene:1017 </v2/query?q=entrezgene:1017>`_
**ensemblgene**               Ensembl gene id                                   `q=ensemblgene:ENSG00000123374 </v2/query?q=ensemblgene:ENSG00000123374>`_
**symbol**                    official gene symbol                              `q=symbol:cdk2 </v2/query?q=symbol:cdk2>`_
**name**                      gene name                                         `q=name:cyclin-dependent </v2/query?q=name:cyclin-dependent>`_
**alias**                     gene alias                                        `q=alias:p33 </v2/query?q=alias:p33>`_
**summary**                   gene summary text                                 `q=summary:insulin </v2/query?q=summary:insulin>`_
**refseq**                    NCBI RefSeq id  (both rna and proteins)           `q=refseq:NM_001798 </v2/query?q=refseq:NM_001798>`_ :raw-html:`<br />`
                                                                                `q=refseq:NP_439892 </v2/query?q=refseq:NP_439892>`_
**unigene**                   NCBI UniGene id                                   `q=unigene:Hs.19192 </v2/query?q=unigene:Hs.19192>`_
**homologene**                NCBI HomoloGene id                                `q=homologene:74409 </v2/query?q=homologene:74409>`_
**accession**                 NCBI GeneBank Accession number                    `q=accession:AA810989 </v2/query?q=accession:AA810989>`_
**ensembltranscript**         Ensembl transcript id                             `q=ensembltranscript:ENST00000266970 </v2/query?q=ensembltranscript:ENST00000266970>`_
**ensemblprotein**            Ensembl protein id                                `q=ensemblprotein:ENSP00000243067 </v2/query?q=ensemblprotein:ENSP00000243067>`_
**uniprot**                   UniProt id                                        `q=uniprot:P24941 </v2/query?q=uniprot:P24941>`_
**ipi**                       PIP id                                            `q=ipi:IPI00031681 </v2/query?q=ipi:IPI00031681>`_
**pdb**                       PDB id                                            `q=pdb:1AQ1 </v2/query?q=pdb:1AQ1>`_
**prosite**                   Prosite id                                        `q=prosite:PS50011 </v2/query?q=prosite:PS50011>`_
**interpro**                  InterPro id                                       `q=interpro:IPR008351 </v2/query?q=interpro:IPR008351>`_
**mim**                       OMIM id                                           `q=mim:116953 </v2/query?q=MIM:116953>`_
**pharmgkb**                  PharmGKB id                                       `q=pharmgkb:PA101 </v2/query?q=pharmgkb:PA101>`_
**reporter**                  Affymetrix probeset id                            `q=reporter:204252_at </v2/query?q=reporter:204252_at>`_
**reagent**                   GNF reagent id                                    `q=reagent:GNF282834 </v2/query?q=reagent:GNF282834>`_
**go**                        Gene Ontology id                                  `q=go:0000307 </v2/query?q=go:0000307>`_
**hgnc**                      HUGO Gene Nomenclature Committee                  `q=hgnc:1771 </v2/query?q=HGNC:1771>`_
**hprd**                      Human Protein Reference Database                  `q=hprd:00310 </v2/query?q=HPRD:00310>`_
**mgi**                       Mouse Genome Informatics                          `q=mgi:MGI\\\\:88339 </v2/query?q=mgi:MGI%5C%5C:88339>`_
**rgb**                       Rat Genome Database                               `q=rgd:620620 </v2/query?q=RGD:620620>`_
**flybase**                   A Database of Drosophila Genes & Genomes          `q=flybase:FBgn0004107&species=fruitfly </v2/query?q=FLYBASE:FBgn0004107&species=fruitfly>`_
**wormbase**                  C elegans and related nematodes database          `q=wormbase:WBGene00057218&species=31234 </v2/query?q=wormbase:WBGene00057218&species=31234>`_
**zfin**                      Zebrafish Information Network                     `q=zfin:ZDB-GENE-980526-104&species=zebrafish </v2/query?q=ZFIN:ZDB-GENE-980526-104&species=zebrafish>`_
**tair**                      Arabidopsis Information Resource                  `q=tair:AT3G48750&species=thale-cress </v2/query?q=TAIR:AT3G48750&species=thale-cress>`_
**xenbase**                   Xenopus laevis and Xenopus tropicalis             `q=xenbase:XB-GENE-1001990&species=frog </v2/query?q=xenbase:XB-GENE-1001990&species=frog>`_

                              biology and genomics resource
**mirbase**                   database of published miRNA sequences and          `q=mirbase:MI0017267 </v2/query?q=mirbase:MI0017267>`_
                              annotation
**retired**                   Retired Entrez gene id, including those            `q=retired:84999 </v2/query?q=retired:84999>`_
                              with replaced gene ids.
========================    =============================================    =================================================================================



Genome interval query
"""""""""""""""""""""

When we detect your query ("**q**" parameter) contains a genome interval pattern like this one::

    chrX:151,073,054-151,383,976

we will do the genome interval query for you. Besides above interval string, you also need to specify "*species*" parameter (with the default as human). These are all acceptted queries::

    q=chrX:151073054-151383976&species:9606
    q=chrX:151,073,054-151,383,976&species:human


.. Hint:: As you can see above, the genomic locations can include commas in it.

.. seealso::

   `Genome assembly information <data.html#genome-assemblies>`_



Wildcard queries
""""""""""""""""
Wildcard character "*" or "?" is supported in either simple queries or fielded queries::

    q=CDK?                              single character wildcard
    q=symbol:CDK?                       single character wildcard within "symbol" field
    q=IL*R                              multiple character wildcard

.. note:: Wildcard character can not be the first character. It will be ignored.


Boolean operators and grouping
""""""""""""""""""""""""""""""

You can use **AND**/**OR**/**NOT** boolean operators and grouping to form complicated queries::

    q=tumor AND suppressor                        AND operator
    q=CDK2 OR BTK                                 OR operator
    q="tumor suppressor" NOT receptor             NOT operator
    q=(interleukin OR insulin) AND receptor       the use of parentheses


Returned object
---------------

A GET request like this::

    http://mygene.info/v2/query?q=symbol:cdk2

should return hits as:

.. code-block:: json

    {
      "hits": [
        {
          "name": "cyclin-dependent kinase 2",
          "_score": 87.76775,
          "symbol": "CDK2",
          "taxid": 9606,
          "entrezgene": 1017,
          "_id": "1017"
        },
        {
          "name": "cyclin-dependent kinase 2",
          "_score": 79.480484,
          "symbol": "Cdk2",
          "taxid": 10090,
          "entrezgene": 12566,
          "_id": "12566"
        },
        {
          "name": "cyclin dependent kinase 2",
          "_score": 62.286797,
          "symbol": "Cdk2",
          "taxid": 10116,
          "entrezgene": 362817,
          "_id": "362817"
        }
      ],
      "total": 3,
      "max_score": 87.76775,
      "took": 4
    }



Batch queries via POST
======================

Although making simple GET requests above to our gene query service is sufficient in most of use cases,
there are some cases you might find it's more efficient to make queries in a batch (e.g., retrieving gene
annotation for multiple genes). Fortunately, you can also make batch queries via POST requests when you
need::


    URL: http://mygene.info/v2/query
    HTTP method:  POST


Query parameters
----------------

q
"""
    Required, multiple query terms seperated by comma (also support "+" or white space), but no wildcard, e.g., 'q=1017,1018' or 'q=CDK2+BTK'

scopes
""""""
    Optional, specify one or more fields (separated by comma) as the search "scopes", e.g., "scopes=entrezgene",
    "scopes=entrezgene,ensemblgene". The available "fields" can be passed to "**scopes**" parameter are
    :ref:`listed above <available_fields>`. Default: "scopes=entrezgene,ensemblgene,retired" (either Entrez
    or Ensembl gene ids).

species
"""""""
     Optional, can be used to limit the gene hits from given species. You can use "common names" for nine common species (human, mouse, rat, fruitfly, nematode, zebrafish, thale-cress, frog and pig). All other species, you can provide their taxonomy ids. See `more details here <data.html#species>`_. Multiple species can be passed using comma as a separator. Default: human,mouse,rat.

fields
""""""
    Optional, can be a comma-separated fields to limit the fields returned from the matching hits.
    If “fields=all”, all available fields will be returned.
    Default: “symbol,name,taxid,entrezgene,ensemblgene”.

Example code
------------

Unlike GET requests, you can easily test them from browser, make a POST request is often done via a
piece of code. Here is a sample python snippet::

    import httplib2
    h = httplib2.Http()
    headers = {'content-type': 'application/x-www-form-urlencoded'}
    params = 'q=1017,1018&scopes=entrezgene'
    res, con = h.request('http://mygene.info/v2/query', 'POST', params, headers=headers)


Returned object
---------------

Returned result (the value of "con" variable above) from above example code should look like this:

.. code-block:: json

    [
      {
        "name": "cyclin-dependent kinase 2",
        "symbol": "CDK2",
        "taxid": 9606,
        "entrezgene": 1017,
        "query": "1017",
        "_id": "1017"
      },
      {
        "name": "cyclin-dependent kinase 3",
        "symbol": "CDK3",
        "taxid": 9606,
        "entrezgene": 1018,
        "query": "1018",
        "_id": "1018"
      }
    ]


.. Tip:: "query" field in returned object indicates the matching query term.

If a query term has no match, it will return with "**notfound**" field as "**true**"::

    params = 'q=1017,dummy&scopes=entrezgene'
    res, con = h.request('http://mygene.info/v2/query', 'POST', params, headers=headers)

.. code-block:: json
    :emphasize-lines: 12

    [
      {
        "name": "cyclin-dependent kinase 2",
        "symbol": "CDK2",
        "taxid": 9606,
        "entrezgene": 1017,
        "query": "1017",
        "_id": "1017"
      },
      {
        "query": "dummy",
        "notfound": true
      }
    ]

If a query term has multiple matches, they will be included with the same "query" field::

    params = 'q=tp53,1017&scopes=symbol,entrezgene'
    res, con = h.request('http://mygene.info/v2/query', 'POST', params, headers=headers)


.. code-block:: json
    :emphasize-lines: 7,15

    [
      {
        "name": "tumor protein p53",
        "symbol": "TP53",
        "taxid": 9606,
        "entrezgene": 7157,
        "query": "tp53",
        "_id": "7157"
      },
      {
        "name": "tumor protein p53",
        "symbol": "Tp53",
        "taxid": 10116,
        "entrezgene": 24842,
        "query": "tp53",
        "_id": "24842"
      },
      {
        "name": "cyclin-dependent kinase 2",
        "symbol": "CDK2",
        "taxid": 9606,
        "entrezgene": 1017,
        "query": "1017",
        "_id": "1017"
      }
    ]







.. raw:: html

    <div id="spacer" style="height:300px"></div>