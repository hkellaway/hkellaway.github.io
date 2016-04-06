# Setup

- Created Xcode project - select the type _Framework & Library_ for your desired platform then select the _Framework_ option. For iOS, that would be _Couch Touch Framework_
- Set the Product Name as whatever the library is to be called
	- For bundle identifier, use what you normally might - for personal projects I use _com.harlankellaway_
	- I elect to include Unit Tests
- Xcode will have created a folder with the project name for you with another folder inside with the same name that houses the libraries files - however, we want the library files to be read from a directory at the same level at the root level of our git repository named something else entirely (in our case, _Sources_) 
- Make the Sources folder
- Copy the files that are in LibraryName/LibraryName to Source (cp -r LibraryName/LibraryName/* Sources/)
- Delete the LibraryName/LibraryName folder (rm -rf LibraryName/LibraryName)
- Move LibraryName.xcodeproj and the LibraryNameTests folder up one level to the root of the git project
- Remove the now broken file references in the Xcode project and drag in the files in Sources/
- I like to set the following Build Settings at the project level: Info.plist (Sources/Info.plist), Bundle Identifier (com.harlankellaway.LibraryName), Product Name (LibraryName)
- Open Build Settings for the specific target and adjust Info.plist, Bundle identifier, and Product Name to inherit from the Project
- Open Build Phases and move LibraryName.h to the Public section under Headers; remove Info.plist from the Copy Bundle Resources section
- You should be able to build without any issue! Tests should also run succesfully (if included)

- I like to rename the initial target LibraryName-iOS if I intend to make the library buildable for any other platform
	- Rename target
	- This will automatically change the Product Name to LibraryName-iOS (instead of the desired LibraryName); change the Product Name explicitly to LibraryName (I like to do this at the Project level)
	- Rename scheme

- Use the following steps for any other platform you intend to support (e.g. tvOS, watchOS)
	- Create new target
	- Select the Framework option for the intended platform
	- Name it LibraryName-PlatformName (e.g. LibraryName-OSX)
	- Update Info.plist, Bundle Identifier, and Product Name to inherit from the Project
	- Remove the LibraryName-OSX folder Xcode generated for that target (we want all targets to read from the same Sources/ folder)
	- Delete the LibraryName-OSX group in Xcode
	- Head to Build Phases and add LibraryName.h under Public Headers
	- Build and tests should pass!

- Lastly, set all the schemes as Shared so the frameworks can be utilized by Carthage
