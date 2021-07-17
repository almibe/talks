# Everyday Linked Data
## Code4Lib 2021

### Abstract

The concept of linked data is now several decades old but is still often treated as a special case by many people working in libraries and archives. This talk will address the benefits of adopting linked data for day to day work; this includes both the advantages of gaining familiarity with the concepts of linked data and the benefits that linked data inherently provides in use. Using existing data and sharing data is made easier by using standard RDF serialization formats. Validating these data and sharing validation rules is handled with the use of SHACL. Querying datasets is provided for with the use of SPARQL. I'll go over several techniques for working with linked data locally and compare them to what is typically being done with relational databases and spreadsheets.

## Notes:

See original gist here, with revision history: https://gist.github.com/almibe/c017fb8f60d9dc136832ff5af265bb0d

## Building

This project uses [marp](https://marp.app/).
See notes on using the marp-cli at https://github.com/marp-team/marp-cli.
Basically try the following.

```
npm install -g @marp-team/marp-cli    #install the marp command (assuming you have npm)
marp pres.md                          #create an html file of the presentation
marp --pdf pres.md                    #create a pdf file
marp -s pres.md                       #live reload the pres and preview @ localhost:5000
```

See the above github project for all of the command's options.
