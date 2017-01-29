# Themeable

[![Build Status](https://travis-ci.org/edwellbrook/Themeable.svg?branch=master)](https://travis-ci.org/edwellbrook/Themeable)

Easy UIKit theming

__Please note:__ This is still a work in progress and not complete. The docs are incomplete and much will be
changing. I recommend not using this in production apps.

## Features

- Type-safe API
- Transparent memory management
- Automatically reuse last used theme
- Thread safe UI updates
- Theme Views and Controls without subclassing
- Extremely flexible (build and load your theme the way that works for you)

## Installation

Installing with [CocoaPods](https://cocoapods.org):

```ruby
# In your Podfile add the following, then
# save and run `pod install`:
pod 'Themeable'
```

## Example Usage

```swift
import UIKit
import Themeable

// Define the theme and its properties to be used throughout your app
struct MyAppTheme: Theme {

    let identifier: String
    let seperatorColor: UIColor
    let lightBackgroundColor: UIColor
    let statusBarStyle: UIStatusBarStyle

    static let light = MyAppTheme(
        identifier: "co.brushedtype.Themeable.light-theme",
        seperatorColor: .lightGray,
        lightBackgroundColor: .white,
        statusBarStyle: .default
    )

    static let dark = MyAppTheme(
        identifier: "co.brushedtype.Themeable.dark-theme",
        seperatorColor: .black,
        lightBackgroundColor: .gray,
        statusBarStyle: .lightContent
    )

    // Expose the available theme variants
    static let variants: [MyAppTheme] = [ .light, .dark ]
    
    // Expose the shared theme manager
    static let manager = ThemeManager<MyAppTheme>(default: .light)

}

// Conform to the `Themeable` protocol and register for updates
class TableViewController: UITableViewController, Themeable {

    override func viewDidLoad() {
        super.viewDidLoad()
        
        // register the themeable items once all the view and subviews
        // have been loaded
        MyAppTheme.manager.register(themeable: self)
    }

    // function will be called whenever the theme changes
    func apply(theme: MyAppTheme) {
        self.tableView.separatorColor = theme.seperatorColor
        self.tableView.backgroundColor = theme.lightBackgroundColor
    }

}
```

## License

The MIT License (MIT)
