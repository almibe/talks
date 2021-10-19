# Ligature Storage

### Abstract

A presentation quickly covering the basics of Ligature and then going over one of the methods used for storing
Ligature's data in a Key-Value store.
A slight variation of the Hexastore architecture is covered as well as several key-stores that work well with this pattern.

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
