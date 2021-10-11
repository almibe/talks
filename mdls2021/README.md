# Introduction to Ligature
## Midwest Data Librarian Symposium 2021

### Abstract

This talk will go over the reasons for the creation of the Ligature knowledge graph specification and related implementations.
Focusing on use cases and practical examples while comparing Ligature to existing options.
Finally a brief status update will be given with plans for future work.

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
