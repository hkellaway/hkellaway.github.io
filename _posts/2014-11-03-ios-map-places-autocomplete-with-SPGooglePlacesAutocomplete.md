---
layout: post
title: iOS Tip - Using SPGooglePlacesAutocomplete for Providing Easy Map Searching with Autocomplete
date: 2014-11-03
categories:
- blog
tags:
- diversityintech
- hackathons
- tech
- transh4ck
status: publish
type: post
published: true
---

The [Google Places Autocomplete](https://developers.google.com/places/documentation/) feature is a great option if you're looking to allow users to search a map - it cuts out a lot of the issues that can arise from users not entering real addresses, entering incomplete addresses, and in you having to implement geocoder calls.

For iOS, one option is using a handy project called *SPGooglePlacesAutocomplete* - which is a "simple objective-c wrapper around the Google Places Autocomplete API." The project I'll be integrating this into already has a map and will display the autocomplete information in a separate view controller, allowing users to select an address and be returned to the map centered on that address.

### Get an API Key

First, an API key for your project will need to be created in the [Google API Console](https://code.google.com/apis/console). NOTE: the type of key created should be a *Server key*, not an *iOS Key*.

### Make Sure Your API Key Works

To test that your API key works, download the SPGooglePlacesAutocomplete project and replace all instances of `YOUR_API_KEY` with your newly generated API key. Then, run the project and make sure you're not getting an error when searching for addresses.

### Add SPGooglePlacesAutocomplete to Your Project

At the time of writing this, the instructions for SPGooglePlacesAutocomplete indicate:

- Copy the following files to your project: *SPGooglePlacesAutocompleteUtilities.h/.m*, *SPGooglePlacesAutocompleteQuery.h/.m*, *SPGooglePlacesPlaceDetailQuery.h/.m*, *SPGooglePlacesAutocompletePlace.h/.m*
- Open *SPGooglePlacesAutocompleteUtilities.h* and replace `kGoogleAPIKey` with your Google API key.

If you're working based off of their view controller example, add *SPGooglePlacesAutocompleteViewController.h/.m* as well.

### Fix Issues

At the time of writing this, SPGooglePlacesAutocomplete was last worked on June 19, 2012. Because of that, a bunch of ARC issues may pop-up among others (e.g. I had to add `#import`s of `<Foundation/Foundation.h>` and '<UIKit/UIKit.h>' in certain files). Resolve these issues and make sure your code builds.

### Create Your View Controller

The sample application provided with SPGooglePlacesAutocomplete uses a .xib file to layout their controller - however, I am partial to *Storyboard*. 

Create your view controller class - lets call it *MapSearchViewController* - it should be a subclass of *UITableViewController*.

Create a new *Table View Controller* in Storyboard and add a *Search Bar and Display Controller* object right underneath the navigation bar. Here's a helpful tutorial on that: [http://www.appcoda.com/search-bar-tutorial-ios7/](http://www.appcoda.com/search-bar-tutorial-ios7/)

Set the *Custom Class* for your new controller as *MapSearchViewController*.

Create `tableView` and `searchBar` outlets in your controller class, as such:

    @property (strong) IBOutlet UITableView *tableView;
    @property IBOutlet UISearchBar *searchBar;

Then make code connections from these outlets to your new controller in *Storyboard*.

### Copy Delegate Method Bodies from Sample Project

The *MapSearchViewController* will be a delegate of [DELEGATES HERE]. The sample project that comes with SPGoogleAutoComplete implements a number of the delegate methods among those:

[LIST OF METHODS]




IMPORTANT: Do not push code to repositories (like GitHub or BitBucket) with your API key intact!





