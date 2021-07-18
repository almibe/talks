# Setting up a Local Linked Data Environment on Your Laptop
## LD4 2021

### Abstract

Having a local environment to experiment with linked data can be a very empowering for both beginner and advanced users. In this session, attendees will learn how to set up a local linked data environment that can be run on a personal desktop computer or laptop, including instruction on running cross platform and open source software for setting up a local RDF store and some helpful related software. The tools for working in these environments will be SPARQL as well as bulk loading datasets.

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
