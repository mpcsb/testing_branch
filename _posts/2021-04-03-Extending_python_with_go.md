---
title:  "Extending python with Go"
excerpt: "A simple example of how GoPy can be used to extend python with Go native code"
header:
  overlay_image: /assets/images/gopy/header.jpg 
tags:
    -  
share: true
subscribe: true
comments: true
--- 


This post is about extending python code with Go.  
Python's ecosystem typically contains a great deal of what is needed, but for the cases when it doesn't or when some bespoke development is justified, Go might be worth looking into. For one, the language is simple and the compiler forces whatever code you generate to maintain some readibility.   
After ad-hoc calls of Go code, structured calls of Go code, trying alternatives like [this](https://www.ardanlabs.com/blog/2020/07/extending-python-with-go.html) or [this](https://medium.com/@andreastagi/extending-python-with-go-part-1-6d0c8bb7dd56), it seems like it can be simpler or just a bit more automated.   
Gopy generates (and compiles) a CPython extension module from a go package. It's well maintained for linux environments and has plenty of examples to learn from. Installing Go and Gopy is straighforward to install and instructions are provided in [Gopy's](https://github.com/go-python/gopy) repository.  
---

To illustrate the process and expose the practical pitfalls of Gopy, let's start with an implementation of a vantage-point tree from the [gonum project](https://github.com/gonum/gonum/blob/master/spatial/vptree/vptree.go).   

First step: have Go code that you want to use in your python pipeline. This bit is an example from gonum that should be simple to follow: essentially from a collection of places and given a specific address, determine which are whithin a certain distance and also to display the top 5 closest distances.   

    package vptree

    import (
      "fmt"
      "log"
      "math"

      "gonum.org/v1/gonum/spatial/vptree"
    )

    func Example_accessiblePublicTransport() {
      // Construct a vp tree of train station locations
      // to identify accessible public transport for the
      // elderly.
      t, err := vptree.New(stations, 5, nil)
      if err != nil {
        log.Fatal(err)
      }

      // Residence.
      q := place{lat: 51.501476, lon: -0.140634}

      var keep vptree.Keeper

      // Find all stations within 0.75 of the residence.
      keep = vptree.NewDistKeeper(0.75)
      t.NearestSet(keep, q)

      fmt.Println(`Stations within 750 m of 51.501476N 0.140634W.`)
      for _, c := range keep.(*vptree.DistKeeper).Heap {
        p := c.Comparable.(place)
        fmt.Printf("%s: %0.3f km\n", p.name, p.Distance(q))
      }
      fmt.Println()

      // Find the five closest stations to the residence.
      keep = vptree.NewNKeeper(5)
      t.NearestSet(keep, q)

      fmt.Println(`5 closest stations to 51.501476N 0.140634W.`)
      for _, c := range keep.(*vptree.NKeeper).Heap {
        p := c.Comparable.(place)
        fmt.Printf("%s: %0.3f km\n", p.name, p.Distance(q))
      }
    }

    // stations is a list of railways stations.
    var stations = []vptree.Comparable{
      place{name: "Bond Street", lat: 51.5142, lon: -0.1494},
      place{name: "Charing Cross", lat: 51.508, lon: -0.1247},
      place{name: "Covent Garden", lat: 51.5129, lon: -0.1243},
      place{name: "Embankment", lat: 51.5074, lon: -0.1223},
      place{name: "Green Park", lat: 51.5067, lon: -0.1428},
      place{name: "Hyde Park Corner", lat: 51.5027, lon: -0.1527},
      place{name: "Leicester Square", lat: 51.5113, lon: -0.1281},
      place{name: "Marble Arch", lat: 51.5136, lon: -0.1586},
      place{name: "Oxford Circus", lat: 51.515, lon: -0.1415},
      place{name: "Picadilly Circus", lat: 51.5098, lon: -0.1342},
      place{name: "Pimlico", lat: 51.4893, lon: -0.1334},
      place{name: "Sloane Square", lat: 51.4924, lon: -0.1565},
      place{name: "South Kensington", lat: 51.4941, lon: -0.1738},
      place{name: "St. James's Park", lat: 51.4994, lon: -0.1335},
      place{name: "Temple", lat: 51.5111, lon: -0.1141},
      place{name: "Tottenham Court Road", lat: 51.5165, lon: -0.131},
      place{name: "Vauxhall", lat: 51.4861, lon: -0.1253},
      place{name: "Victoria", lat: 51.4965, lon: -0.1447},
      place{name: "Waterloo", lat: 51.5036, lon: -0.1143},
      place{name: "Westminster", lat: 51.501, lon: -0.1254},
    }

    // place is a vptree.Comparable implementations.
    type place struct {
      name     string
      lat, lon float64
    }

    // Distance returns the distance between the receiver and c.
    func (p place) Distance(c vptree.Comparable) float64 {
      q := c.(place)
      return haversine(p.lat, p.lon, q.lat, q.lon)
    }

    // haversine returns the distance between two geographic coordinates.
    func haversine(lat1, lon1, lat2, lon2 float64) float64 {
      const r = 6371 // km
      sdLat := math.Sin(radians(lat2-lat1) / 2)
      sdLon := math.Sin(radians(lon2-lon1) / 2)
      a := sdLat*sdLat + math.Cos(radians(lat1))*math.Cos(radians(lat2))*sdLon*sdLon
      d := 2 * r * math.Asin(math.Sqrt(a))
      return d // km
    }

    func radians(d float64) float64 {
      return d * math.Pi / 180
    }   


This is a particularly good example of code to take. The definition of the distance can easily be changed to reflect similarity in words, geometric spaces or whatever rule that makes sense to classify as similar.  

      gopy build -output=some/folder -vm=python3 path/to/go_pkg
      
This creates the shared library and other objects needed for the binding. 

For the the shared objects(.so), there is one extra step before interacting with the bindings, which is to add a new path to the LD_LIBRARY_PATH variable to tell the dynamic link loader where to search for the dynamic shared libraries. There is a long lasting [issue](https://github.com/go-python/gopy/issues/203), where all steps are descbribed.  
If you're in the location of the generated folder add the current working directory ($PWD) to the environment variable, else adjust it accordingly.

      LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$PWD python3

After it, you're free to import vptree and use it with little to no issues.    


        Python 3.7.6 (default, Jan  8 2020, 19:59:22) 
        [GCC 7.3.0] :: Anaconda, Inc. on linux
        Type "help", "copyright", "credits" or "license" for more information.
        >>> import vptree
        >>> vptree.Example_accessiblePublicTransport()
        Stations within 750 m of 51.501476N 0.140634W.
        St. James's Park: 0.545 km
        Green Park: 0.600 km
        Victoria: 0.621 km

        5 closest stations to 51.501476N 0.140634W.
        St. James's Park: 0.545 km
        Green Park: 0.600 km
        Victoria: 0.621 km
        Hyde Park Corner: 0.846 km
        Picadilly Circus: 1.027 km

--- 

Simple enough.
This was a very simple example, but it seems to generalize well to more complex Go code.   
